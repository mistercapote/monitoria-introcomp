# 🛠️ Guia de Sobrevivência: Sed & Grep

Este documento contém referências rápidas para a edição e transformação de fluxos de texto com **Stream Editor** e para a busca e filtragem de padrões de texto com **Global Regular Expression Print**.

## ✂️ Stream Editor (sed)
O `sed` é um editor de texto não interativo. Ele recebe um fluxo de dados (um arquivo ou a saída de outro comando), realiza transformações linha a linha conforme regras definidas e exibe o resultado.

### Anatomia

`sed -OPÇÕES 'ENDEREÇO/FLAGS COMANDO/BUSCA/SUBSTITUIÇÃO/FLAGS' ARQUIVO`

*Apenas os campos ENDEREÇO e BUSCA aceitam regex e flags.*

#### 📋 Comandos
| Categoria | Comando | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- | 
| **Substituir** | `s/A/B/` | Em cada linha, troca a primeira ocorrência de **A** por **B**. | `sed 's/a/A/' arquivo.txt` | O primeiro "a" de cada linha se torna maiúsculo.
| **Transliterar** | `y/A/B/` | Troca TODAS as ocorrências de cada caractere de **A** pelo correspondente em **B**. Não permite uso de regex. Comprimento de **A** deve ser o mesmo de **B**| ` sed 'y/áéíóú/aeiou/' arquivo.txt` | Remove acentos agudos das vogais.
| **Deletar** | `/A/d` | Apaga as linhas que contenham **A** | `sed '/^$/d' dados.csv` | Deleta linhas vazias
| **Inserir** | `/A/i B` | Insere uma linha **antes** das linhas que contenham **A** com texto **B**. | `sed '1i Nome,Idade' dados.csv` | Adiciona o cabeçalho **antes** da primeira linha.
| **Anexar** | `/A/a B` | Adiciona uma linha **após** das linhas que contenham **A** com texto **B**. | `sed '$a Fim do arquivo' arquivo.txt` | Adiciona o rodapé **após** a última linha.

#### 📋 Flags
| Categoria | Flag | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Global** | `s/A/B/g` | Em cada linha, troca TODAS as ocorrências de **A** por **B**. | `sed 's/a/A/g' arquivo.txt` | Todos os "a" se tornam maiúsculos.
| **Ocorrência** | `s/A/B/n` | Em cada linha, troca a n-ésima ocorrência de A por B.| `sed 's/a/A/2'` | O segundo "a" de cada linha se torna maiúsculo. |
| **Imprimir** | `s/A/B/p` | Imprime apenas o que for solicitado. | `sed -n 's/A/B/p'` | Imprime a linha **apenas se** a substituição ocorrer. |
| **Ignorar Case (Busca)** | `/A/B/i` | Qualquer variação de case da Busca | `sed 's/casa/lar/i' arquivo.txt` | Não importa se é "Casa", "casa", "CaSA", "caSA", todos se tornam "lar".
| **Ignorar Case (Endereço)**  | `/A/I` | Qualquer variação de case do Endereço  | `sed '/casa/I d' dados.csv` | Deleta linhas com "Casa", "casa", "CaSA", "caSA".
| **Negação** | `!` | Inverte o critério de seleção. | `sed -n '/texto/!p'` | Mostra linhas que **NÃO** contêm "texto". |

#### 📋 Endereço
| Categoria | Endereço | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Número** | `n` |Aplica o comando apenas na linha **n**. | `sed '2s/A/B/'` | Apenas na linha 2, troca a primeira ocorrência de **A** por **B**. |
| **Intervalo** | `n,m` | Aplica o comando da linha **n** até a **m**. | `sed '1,5d'` | Deleta da linha 1 a 5 |
| **Salto** | `n~m` | Começa em **n** e pula de **m** em **m**. | `sed -n '1~2p'` | Mostra linhas ímpares. |

#### 📋 Opções
| Categoria | Opção | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Silencioso** | `-n` | Inibe a impressão automática de todas as linhas. Usado quase sempre com a flag `p` para mostrar apenas o necessário. | `sed -n '1,5p'` | Imprime apenas as 5 primeira linhas |
| **Múltiplos** | `-e` | Permite executar vários comandos em sequência. | `sed -e 's/a/A/' -e 's/b/B/' dados.csv` |
| **Salvar** | `-i` | Salva as mudanças direto no arquivo (in-place). | `sed -i 's/old/new/' dados.csv` |
| **Regex Estendida** | `-E` ou `-r` | Habilita Regex moderna, permitindo usar `( )`, `\|`, `+` e `?` sem barras invertidas. | `sed -E 's/(a\|b)/X/'` | |


### Agrupamento de Comandos 

Se você quer que o `sed` faça várias coisas apenas em um endereço específico, use `{ }`. Funciona como um bloco `if`.

`sed '/ENDEREÇO/FLAGS { c1; c2; c3; ... }' ARQUIVO`

| Exemplo | Explicação |
| :--- | :--- |
| `sed '/erro/I { s/falha/FIX/; s/bug/CORRECAO/; }'` | Nas linhas com "erro" (ignore case), faz duas trocas diferentes. |
| `sed '1,5 { s/X/Y/; d; }'` | Nas linhas 1 a 5, tenta trocar X por Y e depois deleta a linha. |
| `sed '/^$/ { i \---; a \--- }'` | Em linhas vazias, insere uma linha de traços antes e anexa outra depois.

## 🎯 Global Regular Expression Print (grep)
O `grep` é uma ferramenta de busca que utiliza de expressões regulares para encontrar padrões e filtrar o texto.

### Anatomia do Comando

`grep -OPÇÕES 'PADRÃO' ARQUIVO`

#### 📋 Opções 
| Categoria | Opção | Descrição | Exemplo |
| :--- | :---: | :--- | :--- |
| **Regex Estendida**| `-E` | Habilita Regex moderna (evita o uso de barras `\`).| `grep -E "A\|B"` |
| **Ignorar Case** | `-i` | Busca sem diferenciar maiúsculas de minúsculas. | `grep -i "erro" log.txt` |
| **Palavra Exata** | `-w` | O padrão deve ser uma palavra inteira (isolada). | `grep -w "ana" arq` |
| **Linha Exata** | `-x` | A linha inteira deve ser idêntica ao padrão. | `grep -x "fim" arq` |
| **Limite de Matches**| `-m n` | Para de buscar após encontrar **n** ocorrências. | `grep -m 1 "erro" log.txt` |
| **Número da Linha**| `-n` | Exibe o número da linha onde o padrão foi achado. | `grep -n "segfault" debug.txt` |
| **Destacar Arquivo** | `-H` | Sempre mostra o nome do arquivo (mesmo em um só arquivo). | `grep -H "erro" log.txt` |
| **Omitir Arquivo** | `-h` | Não mostra o nome do arquivo no início da linha. | `grep -h "erro" *.log` |
| **Apenas o Match** | `-o` | Exibe apenas o texto exato que casou, não a linha toda. | `grep -o "[0-9]\+" dados.txt` |
| **Silencioso** | `-q` | Não exibe nada. Útil para testes em scripts (`if`). | `grep -q "A" arq` |
| **Contar** | `-c` | Exibe apenas o número de linhas que deram match. | `grep -c "ERROR" server.log` |
| **Listar Matches**| `-l` | Exibe apenas o nome dos arquivos que contêm o padrão. | `grep -l "main" *.c` |
| **Listar Não-Matches**| `-L` | Exibe apenas o nome dos arquivos que **NÃO** têm o padrão. | `grep -L "licenca" *.txt` |
| **Recursivo** | `-r` | Busca em todos os arquivos de uma pasta e subpastas. | `grep -r "TODO" ./src` |
| **After** | `-A n` | Exibe a linha encontrada e as **n** linhas **depois**. | `grep -A 3 "erro" log.txt` |
| **Before** | `-B n` | Exibe a linha encontrada e as **n** linhas **antes**. | `grep -B 2 "func main" main.c` |
| **Context** | `-C n` | Exibe a linha e **n** linhas em volta (antes e depois). | `grep -C 5 "panic" log.txt` |
| **Suprimir Erros** | `-s` | Não mostra avisos de arquivos inexistentes ou ilegíveis. | `grep -s "busca" *.txt` |
| **Inverter** | `-v` | Exibe as linhas que **NÃO** contêm o padrão. | `grep -v "^#" config.conf` |
| **Múltiplos padrões**| `-e` | Permite buscar por vários padrões diferentes. | `grep -e "A" -e "B" arquivo.txt` |
| **Colorir** | `--color` | Destaca o termo encontrado com cores no terminal. | `grep --color=auto "alvo" arq` |
