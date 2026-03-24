# 🛠️ Guia de Sobrevivência: Grep

Este documento contém referências rápidas para a busca e filtragem de padrões de texto com Global Regular Expression Print.

---

## 🔍 Global Regular Expression Print (grep)
O `grep` é uma ferramenta de busca que utiliza de expressões regulares para encontrar padrões e filtrar o texto.

### Anatomia do Comando

`grep -OPÇÕES 'PADRÃO' ARQUIVO`

---

## 📋 Opções
As opções mudam como o `grep` busca ou o que ele exibe após encontrar o padrão.

| Categoria | Opção | Descrição | Exemplo |
| :--- | :---: | :--- | :--- |
| **Ignorar Case** | `-i` | Busca sem diferenciar maiúsculas de minúsculas. | `grep -i "erro" log.txt` |
| **Recursivo** | `-r` | Busca em todos os arquivos de uma pasta e subpastas. | `grep -r "TODO" ./src` |
| **Inverter** | `-v` | Exibe as linhas que **NÃO** contêm o padrão. | `grep -v "^#" config.conf` |
| **Contar** | `-c` | Exibe apenas o número de linhas que deram match. | `grep -c "ERROR" server.log` |
| **Listar Arquivos**| `-l` | Exibe apenas o nome dos arquivos que contêm o padrão. | `grep -l "main" *.c` |
| **Número da Linha**| `-n` | Exibe o número da linha onde o padrão foi achado. | `grep -n "segmentation fault" debug.txt` |
| **Apenas o Match** | `-o` | Exibe apenas o texto exato que casou com a regex. | `grep -o "[0-9]\+" dados.txt` |
| **Regex Estendida**| `-E` | Habilita Regex moderna (mesmo que usar o comando `egrep`).| `grep -E "A\|B"` |
| **After** | `-A n` | Exibe a linha encontrada e as **n** linhas **depois**. | `grep -A 3 "erro" log.txt` |
| **Before** | `-B n` | Exibe a linha encontrada e as **n** linhas **antes**. | `grep -B 2 "func main" main.c` |
| **Context** | `-C n` | Exibe a linha e **n** linhas em volta (antes e depois). | `grep -C 5 "panic" log.txt` |
