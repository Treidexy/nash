### symbols
- auto file namespace (like `cargo`-ish)
- reference symbol `let fs => std::filesystem;`
- easy linking?
- multiple names `fn absolute_value abs(?) -> ?`
- private by default (explicit `pub`)
- delete name `@delete std::filesystem;`
- friend `struct Bogus { pub(Fred, Joe) my_thing: u32 } struct Fred {} struct Joe {}`
- abstract symbol `let mut thing = $getHat; if no_hat() { thing = $getHair; } mynamespace::MyStruct::(thing)(self);` evals to `mynamespace::MyStruct::getHat(self) else no_hat() { mynamespace::MyStruct::getHair(self) }`
- weird name `let ``space case rocks`` = 69_420;` // single `, but markdown sucks
### abstraction
- templates? ~ obselete by trait system?? `fn min<T>(a: T, b: T) -> T`
- depleeted functions `fn min(a: impl Integer, b: @skele Integer, c: dyn Integer) -> ?`
- depleeted structs `impl Integer` = `T: Integer` vs `@skele Integer = struct { func: *fn(), }` vs `dyn Integer` = `struct { self: *u8, skele: @skele Integer, }`?
- trait of impl `trait Int { fn inc(mut self); }` `impl Int { fn inc(mut self) { self++; } }`
### functions
- special functions? `fn @special climb(code: i32)` `impl climb(code = 69) { ... }`
- owned parameter `fn (mine: &String)`? or `fn (&mine: String)`?
- nameless params `fn(param: u64, u64)`
- abstract (code determined) return value `fn() -> ?`
- abstract params `fn(param: ?) -> i32`
- multi-return `fn(param: ?) -> (a: i32, b: ?)`
- optional return `fn() -> (a?: i32)`
- one-liner `fn muladd(a: f64, b: f64, c: f64) -> a + b * c;`
- lambda `fn() -> (?) { ... }`
- scope function? `fn something(p: *u8) { fn' count_len(p) -> (len: u64) { len = 0; loop p[len] != 0 { len++; } } }`
- named arguments `make_rect(top: 0, left: 0, bottom: 100, right: 64)`?
- slated functions `let square = pow(, 2);`+
- fixed len fn/scope `fn' (0x1000) my_scope()` // function is code + padding to make 0x1000 bytes long total
- fixed address `fn &(0x401000) _start()` or `fn &(&get_cheese + 0x5500) eat_cheese()`
- no return `fn panic(msg: *struct String) -> !;`
- cool example: `fn &(0x401000) (0xff) _start(argc (%rsp[0]): i32, argv (%rsp[8]): [*u8; argc]) -> ! {}`?
- default args `fn peek(offset: i64 = 0);`
### types
- struct `struct Vec2 (0x40) { x: f64 align 16, y: f64 align 8 size 8, }`
- trait `trait Add<T: type> { let OutType: type; fn add(self, T) -> OutType; }`
- see abstraction::slated traits
- enum `enum Number { One = 1, Two, Three = 3, Four, }`
- samesh enum `enum Number { One = 2, Two = 3 { name: String }, }`
- flags `enum @flags Perms { Read = 0, Write = 1, Exec = 2, ReadWrite = Perms::Read | Perms::Write /* 0b011 */ }`? // use number to specify idx of bit
- samesh (unions) `@samesh Vec2, struct { u64, u64 };`?
- shadow? `struct TypeId = u64;`
- `type` type
- `namespace` type?
- `symbol` type
- ptr type `*mut u64`
- array `[u8; 69_420]`
- nameless struct (var) `let game_input: struct (0x8) { left: bool, right: bool };`
- struct of `let old_state: struct &game_state;`
- fn type `fn (0x64) (x: u64) -> (y?: u64)` // 0x64 byte function struct
### variables
- immutible by default
- explicit undefined initialization `let x: u32; // not allowed` vs `let x: u32 = ?; // yes allowed`
- register+ `let ptr %ax: *u8 = ?;`
- global (constants) `const str: u64 = "";`, `const mut block: [u8; 64] = [2u8; 64];`?
- eval var `let curr => self.src[self.pos];`
### expressions
- array indexing `array[idx]` or `array[] == array[0]`
- deref? `*p` equivalent to `p[]`
- addr of `&p`
- pass/transfer ownership `^mystring`
- comptime eval `let pi = const arcsin(0);`
- array/slice init `[0, 1, 2, 3]`
- casting `f64::from(0xff77)` `0xff77.into<f64>()`
### literals
- seperators `0b11100010_00011010`
- hex/bin floats `0xff794201_f32` // `_` required
- multiline string by default
- symbol frag `$my_thing`
### tooling
- easy refactoring
- find references, usages, assignments, muts, etc
- scope popping [direct from code]
- frame popping (functions & scopes)
- messy code meter :)
- documentation freak // do ur docs
- code baking ~ `let x = some_long_thing_with_vague_return_type();` -> `let x: BogoType = some_long_thing_with_vague_return_type();`
### misc
- everything is expr
- rules? `@rule glGetError() == 0` // ran after each line? // maybe obselete from pure scopes?
- easy refactoring ;)
- comptime if/match? `if const DEBUG { ... }` `match const TARGET_FRUIT { Grape -> ..., Banana -> ..., ... }` // obselete by good optimizer?
- delete keyword `@delete if`  // `@if` is still usable
- ERROR HANDLING???
- pass by reference is default (ownership transfer must be explicit)
- auto enum detection `enum LongName { Yes, No, Maybe, } fn do_thing(x: i32) -> LongName { return match x { 0 => Yes, 1 => No, 2 => LongName::Maybe, } }`

