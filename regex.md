# 🛠️ Guia de Sobrevivência: Regex

Este documento contém referências rápidas para extração de padrões com Expressões Regulares.


## 🔍 Expressões Regulares (Regex)
O Regex é uma ferramenta para identificar, manipular e extrair padrões de texto.

### Guia de Caracteres Especiais

| Categoria | Caractere | Descrição | Exemplo | Explicação
| :--- | :--- | :--- | :--- | :--- |
| **Âncoras** | `^` | Início da linha | `^A` | Encontra linha começando com A |
|  | `$` | Final da linha | `z$` | Encontra linha terminando em z |
|  | `\b` | Fronteira de palavra | `\bpedra\b` | Encontra "pedra", mas não "enpedrada"
|  | `\B` | NÃO-fronteira de palavra | `\Bpedra\B` | Encontra "enpedrada", mas não "pedra" |
| **Classes** | `.` | Qualquer caractere | `g.t.` | Encontra "gota", "gato", "gata" |
|  | `\d` | Qualquer dígito numérico | `\d{2}` | Encontra "12", '55", "00" |
|  | `\D` | Qualquer caractere NÃO numérico | `\D{3}` | Encontra "a-o", "ola", " de" |
|  | `\w` | Alfanumérico (letras, números e `_`) | `\w{3}` | Encontra "B_9", "A22", "e3D" |
|  | `\W` | NÃO-alfanumérico (símbolos) | `\W` | Encontra "@", "#", "!" |
|  | `\s` | Espaço em branco |  |
|  | `\S` | Qualquer caractere NÃO espaço |  |
|  | `\n` | Quebra de linha  |  |
|  | `\t` | Tabulação (Tab) |  |
| **Classes POSIX** | `[[:alpha:]]` | Qualquer letras (considera acentos) |  |
|  | `[[:alnum:]]` | Alfanumérico (letras, números e `_`) |  |
|  | `[[:digit:]]` | Qualquer dígito numérico |  |
|  | `[[:space:]]` | Espaços, tabs e quebras de linha.
| **Conjuntos** | `[abc]` | Qualquer um dos caracteres especificados | `[aeiou]` | Encontra vogais |
|  | `[^abc]` | Qualquer caractere EXCETO os especificados | `[^aeiou]` | Encontra consoantes |
|  | `[a-z]` | Intervalo de caracteres | `[0-5]` | Encontra números de 0 a 5 |
| **Quantificadores** | `*` | Zero ou mais ocorrências | `lo*` |Encontra "l", "lo", "looo" |
|  | `+` | Uma ou mais ocorrências | `lo+` | Encontra "lo", "looo" |
|  | `?` | Zero ou uma ocorrência (opcional) | `casas?` | Encontra "casa", "casas" |
|  | `{n}` | Exatamente **n** ocorrências | `\d{2}` | Encontra "12", '55", "00" |
|  | `{n,m}` | De **n** até **m** ocorrências | `\d{2,4}` | Encontra "10", "173", "0024" |
| **Lógica** | `(...)` | Agrupamento e captura | `(banana)` | Encontra "banana", valor fica salvo em `\1`. Se houver outro `(...)`, valor fica salvo em `\2` e assim por diante. |
| | `(?:...)` | Agrupamento sem captura | `(?:banana)` | Encontra "banana", mas valor não fica salvo em memória. |
|  | `\1`, `\2`... | Recupera o conteúdo dos grupos capturados. | `sed -E 's/(.*) (.*)/\2, \1/'` | Inverte primeira e segunda palavra da de cada linha |
|  | `&` | Representa **todo** o texto que deu match. | `sed 's/palavra/[&]/g'` | Colocar `[]` em volta de "palavra" |
|  | `\|` | Operador OU | `(banana\|maçã)` | Encontra "banana", "maçã"|
|  | `\` | Escape (anula o poder do símbolo) | `\.` | Encontra "." |

