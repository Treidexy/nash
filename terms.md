Before parsing, but after lexing. Terms will be used as a layer above Tokens to aid in parsing. Here are the types of terms:

### Tuples
- opened and closed by paren
- elements seperated by comma
- each element has a part before the colon and after
- colon is optional
- ej: `(name, four five: lol)`

### Blocks
- opened and closed by braces
- elements seperated by semi
- ej: `{ print lol; sing a song; jk }`

### Lists
- opened and closed by brackets
- elements seperated by comma
- ej: `[ the, sky is, blue today ]`

### Tokens
- everything else stay as tokens
