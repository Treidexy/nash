### symbols
- auto file namespace (like `cargo`-ish)
- reference symbol `let fs => std::filesystem;`
- easy linking?
- multiple names `fn absolute_value abs(?) -> ?`
- private by default (explicit `pub`)
- delete name `@delete std::filesystem;`
### abstraction
- templates? ~ obselete by trait system?? `fn min<T>(a: T, b: T) -> T`
- slated functions `fn min(a: struct Integer, b: struct Integer) -> ?`
- slated traits `impl Integer` = `T: Integer` vs `struct Integer` = `struct { func: *fn(), }`?
- trait of impl `trait Int { fn inc(*mut self); }` `impl Int { fn inc(*mut self) { self++; } }`
### functions
- nameless params `fn(param: u64, u64)`
- abstract (impl-specific) return value `fn() -> ?`
- abstract params `fn(param: ?) -> i32`
- multi-return `fn(param: ?) -> (a: i32, b: ?)`
- optional return `fn() -> (a?: ?)`
- one-liner `fn muladd(a: f64, b: f64, c: f64) -> a + b * c;`
- lambda `fn() -> (?) { ... }`
- scope function `fn something(p: *u8) { fn' count_len(p) -> (len: u64) { len = 0; loop [len]p != 0 { len++; } } }`
- named arguments `make_rect(top: 0, left: 0, bottom: 100, right: 64)`?
### types
- struct `struct Vec2 (0x40) { x: f64 align 16, y: f64 align 8 size 8, }`
- trait `trait Add<T: type> { let OutType: type; fn add(self, &T) -> OutType; }`
- see abstraction::slated traits
- enum `enum Number { One = 1, Two, Three = 3, Four, }`
- flags `enum @flags Perms { Read, Write, Exec, ReadWrite = Perms::Read | Perms::Write }`?
- samesh (unions) `@samesh Vec2, struct { u64, u64 };`
- samesh enum `enum Number { One = 2, Two = 3 { name: String }, }`
- shadow `struct TypeId = u64;`
- `type` type
- `namespace` type?
- ptr type `*mut u64`
- array `[u8; 69_420]`
- nameless struct (var) `let game_input: struct (0x8) { left: bool, right: bool };`
- struct of `let old_state: struct &game_state;`
- fn type `fn (0x64) (x: u64) -> (y?: u64)` // 0x64 byte long function struct
### variables
- immutible by default
- explicit undefined initialization `let x: u32; // not allowed` vs `let x: u32 = ?; // yes allowed`
- register? `let ptr %ax: *u8 = ?;`
- global (constants) `const str: u64 = "";`, `const mut block: [u8; 64] = [2u8; 64];`
- eval var `let curr => self.src[self.pos];`
### expressions
- array indexing `array[idx]`
- deref `*array`
- implicit address access `smth.idx: *u64` vs `*smth.idx: u64`
- comptime eval `let pi = const arcsin(0);`
- array/slice init `[0, 1, 2, 3]`
- casting `f64::from(0xff77)` `0xff77.into<f64>()`
- pass/transfer ownership `&mystring`
### literals
- seperators `0b11100010_00011010`
- hex/bin floats `0xff794201_f32` // `_` required
- multiline string by default
### tooling
- easy refactoring
- find references, usages, assignments, muts, etc
- scope popping [direct from code]
### misc
- everything is expr
- rules `@rule glGetError() == 0` // ran after each line? // maybe obselete from pure scopes?
- easy refactoring ;)
- comptime if/match `if const DEBUG { ... }` `match const TARGET_FRUIT { Grape -> ..., Banana -> ..., ... }`
- ERROR HANDLING???
