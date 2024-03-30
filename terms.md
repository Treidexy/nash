Before parsing, but after lexing. Terms will be used as a layer above Tokens to aid in parsing. Here are the types of terms:

### Tuples
- opened and closed by paren
- elements seperated by comma
- each element are in the form `_ : _ = _`
- ej: `(name, four five: lol = 69)`

### Blocks
- opened and closed by braces
- elements seperated by semi
- ej: `{ print lol; sing a song; jk { another block }; no need for another semi at the end! }`

### Lists
- opened and closed by brackets
- elements seperated by comma
- ej: `[ the, sky is, blue today ]`

### Tokens
- everything else stay as tokens
