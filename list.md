### symbols
- auto file namespace (like `cargo`-ish)
- symbol renaming?
- easy linking?
- multiple names `fn absolute_value abs(?) -> ?`
### functions
- nameless params `fn(param: u64, u64)`
- abstract (impl-specific) return value `fn() -> ?`
- abstract params `fn(param: ?) -> i32`
- multi-return `fn(param: ?) -> (a: i32, b: ?)`
- optional return `fn() -> (a?: ?)`
- one-liner `fn muladd(a: f64, b: f64, c: f64) -> a + b * c;`
- lambda `fn() -> (?) { ... }`
- scope function `fn something(p: *u8) { fn' count_len(p) -> (len: u64) { len = 0; loop [len]p != 0 { len++; } } }`
- comptime eval `let pi = const arcsin(0);`
### types
- struct `struct Vec2 (0x40) { x: f64 align 16, y: f64 align 8 size 8, }`
- trait `trait Add<T: type> { let OutType: type; fn add(self, &T) -> OutType; }`
- enum `enum Number { One = 1, Two, Three = 3, Four, }`
- flags `enum @flags Perms { Read, Write, Exec, ReadWrite = Perms::Read | Perms::Write }`?
- samesh (unions) `@samesh Vec2, struct { u64, u64 };`
- samesh enum `enum Number { One = 2, Two = 3 { name: String }, }`
- shadow `struct TypeId = u64;`
- `type` type
### variables
- immutible by default
- explicit undefined initialization `let x: u32; // not allowed` vs `let x: u32 = ?; // yes allowed`
- register? `let ptr %ax: *u8 = ?;`
- global (constants) `const str: u64 = "";`, `const mut block: [u8; 64] = [2u8; 64];`
### expressions
- array indexing `[idx]array`
- deref `*array`
- implicit address access `smth.idx: *u64` vs `*smth.idx: u64`
### misc
- everything is expr
- multiline string by default
- easy refactoring ;)
