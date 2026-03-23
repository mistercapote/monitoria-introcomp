# 🛠️ Guia de Sobrevivência: Sed


Este documento contém referências rápidas para a edição e transformação de fluxos de texto com Stream Editor (sed)**.

---

## ✂️ Stream Editor (sed)
O `sed` é um editor de texto não interativo. Ele recebe um fluxo de dados (um arquivo ou a saída de outro comando), realiza transformações linha a linha conforme regras definidas e exibe o resultado.

### Anatomia

`sed -OPÇÕES 'ENDEREÇO/FLAGS COMANDO/BUSCA/SUBSTITUIÇÃO/FLAGS' ARQUIVO`

*Apenas os campos ENDEREÇO e BUSCA aceitam regex e flags.*


### 📋 Comandos

| Categoria | Comando | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- | 
| **Substituir** | `s/A/B/` | Em cada linha, troca a primeira ocorrência de **A** por **B**. | `sed 's/a/A/' arquivo.txt` | O primeiro "a" de cada linha se torna maiúsculo.
| **Transliterar** | `y/A/B/` | Troca TODAS as ocorrências de cada caractere de **A** pelo correspondente em **B**.| ` sed 'y/áéíóú/aeiou/' arquivo.txt` | Remove acentos agudos das vogais.
| **Deletar** | `/A/d` | Apaga as linhas que contenham **A** | `sed '/^$/d' dados.csv` | Deleta linhas vazias
| **Inserir** | `/A/i B` | Insere uma linha **antes** das linhas que contenham **A** com texto **B**. | `sed '1i Nome,Idade' dados.csv` | Adiciona o cabeçalho **antes** da primeira linha.
| **Anexar** | `/A/a B` | Adiciona uma linha **após** das linhas que contenham **A** com texto **B**. | `sed '$a Fim do arquivo' arquivo.txt` | Adiciona o rodapé **após** a última linha.


### 📋 Flags
| Categoria | Flag | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Global** | `s/A/B/g` | Em cada linha, troca TODAS as ocorrências de **A** por **B**. | `sed 's/a/A/g' arquivo.txt` | Todos os "a" se tornam maiúsculos.
| **Ocorrência** | `1`, `2`, ... | Em cada linha, troca a n-ésima ocorrência de A por B.| `sed 's/a/A/2'` | O segundo "a" de cada linha se torna maiúsculo. |
| **Imprimir** | `s/A/B/p` | Imprime apenas o que for solicitado | `sed -n 's/A/B/p'` | Imprime a linha **apenas se** a substituição ocorrer. |
| **Ignorar Case** | `s/A/B/i` | Em cada linha, troca a primeira ocorrência de qualquer variação de case de **A** por **B**. | `sed 's/casa/lar/i' arquivo.txt` | Não importa se é "Casa", "casa", "CaSA", "caSA", todos se tornam "lar".
|  | `/A/I d B` | Apaga as linhas que contenham qualquer variação de case de **A**  | `sed '/casa/d' dados.csv` | Deleta linhas com "Casa", "casa", "CaSA", "caSA".
|  | `/A/I i B` | Insere uma linha **antes** das linhas que contenham qualquer variação de case de **A** com texto **B**. |  | 
|  | `/A/I a B` | Adiciona uma linha **após** das linhas que contenham qualquer variação de case de **A** com texto **B**. |  | 


### 📋 Opções
| Categoria | Opção | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Múltiplos** | `-e` | Permite executar vários comandos em sequência. | `sed -e 's/a/A/' -e 's/b/B/' dados.csv` |
| **Salvar** | `-i` | **Edição in-place**: Salva as mudanças direto no arquivo. | `sed -i 's/old/new/' dados.csv` |

## 📍 Endereço
| Categoria | Endereço | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Número** | `1`, `2`, ... |Aplica o comando apenas na linha **n**. | `sed '2s/A/B/'` | Apenas na linha 2, troca a primeira ocorrência de **A** por **B**. |
| **Intervalo** | `n,m` | Aplica o comando da linha **n** até a **m**. | `sed '1,5d'` | Deleta da linha 1 a 5 |
| **Regex** | | Aplica o comando apenas em linhas que contêm o padrão. | `sed '/C/ s/A/B/'` | Apenas nas linhas que contêm **C**, troca a primeira ocorrência de **A** por **B**. |

---

## 🧠 Lógica de Grupos e Retrovisores

Ao usar parênteses de captura, você pode reutilizar partes do texto encontrado:

| Sintaxe | Função | Exemplo |
| :--- | :--- | :--- |
| `\1, \2...` | Recupera o conteúdo dos grupos capturados. | `sed -E 's/(.*) (.*)/\2, \1/'` (Inverte Nome Sobrenome) |
| `&` | Representa **todo** o texto que deu match. | `sed 's/palavra/[&]/g'` (Coloca colchetes em volta) |


