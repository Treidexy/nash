```zig
pub fn adjacent(self: Square) Area {
    var area = Area.initEmpty();

    for ([_]isize{ -1, 0, 1 }) |dy| {
        for ([_]isize{ -1, 0, 1 }) |dx| {
            if (dx == 0 and dy == 0) continue;

            const x = @as(isize, @intCast(self % width)) + dx;
            const y = @as(isize, @intCast(self / width)) + dy;

            if (x < 0 or x >= width or y < 0 or y >= height) {
                continue;
            }

            area.set(@intCast(x + y * width));
        }
    }

    return area;
}
```

```sy
pub adjacent = (.from: Square) -> (.area: Area = Area.initEmpty()) {
    for dy in Range(-1, 1) {
        for dx in Range(-1, 1) {
            continue if dy == dx == 0;

            const x = (from % width).into(isize) + dx;
            const y = (from / width).into(isize) + dy;

            continue if x nin Range(0, width) or y nin Range(0, height);

            area(x + y * width) = true;
        }
    }
}
```

---

```cpp
Value Eval::evaluate(const Eval::NNUE::Networks&    networks,
                     const Position&                pos,
                     Eval::NNUE::AccumulatorCaches& caches,
                     int                            optimism) {

    assert(!pos.checkers());

    int  simpleEval = simple_eval(pos, pos.side_to_move());
    bool smallNet   = std::abs(simpleEval) > SmallNetThreshold;
    int  nnueComplexity;
    int  v;

    Value nnue = smallNet ? networks.small.evaluate(pos, &caches.small, true, &nnueComplexity)
                          : networks.big.evaluate(pos, &caches.big, true, &nnueComplexity);

    const auto adjustEval = [&](int nnueDiv, int pawnCountConstant, int pawnCountMul,
                                int npmConstant, int evalDiv, int shufflingConstant) {
        // Blend optimism and eval with nnue complexity and material imbalance
        optimism += optimism * (nnueComplexity + std::abs(simpleEval - nnue)) / 584;
        nnue -= nnue * (nnueComplexity * 5 / 3) / nnueDiv;

        int npm = pos.non_pawn_material() / 64;
        v       = (nnue * (npm + pawnCountConstant + pawnCountMul * pos.count<PAWN>())
             + optimism * (npmConstant + npm))
          / evalDiv;

        // Damp down the evaluation linearly when shuffling
        int shuffling = pos.rule50_count();
        v             = v * (shufflingConstant - shuffling) / 207;
    };

    if (!smallNet)
        adjustEval(32395, 942, 11, 139, 1058, 178);
    else
        adjustEval(32793, 944, 9, 140, 1067, 206);

    // Guarantee evaluation does not hit the tablebase range
    v = std::clamp(v, VALUE_TB_LOSS_IN_MAX_PLY + 1, VALUE_TB_WIN_IN_MAX_PLY - 1);

    return v;
}
```

```sy
pub evaluate = (
	.: mut Eval,
	.networks: Eval.NNUE.Networks,
	.pos: Position,
	.caches: mut Eval.NNUE.AccumulatorCaches,
	.optimism: int,
) -> (.v: Value) {
	const simpleEval = simple_eval(pos, pos.side_to_move());
	const smallNet = std.abs simpleEval > SmallNetThreshold;
	var nnueComplexity = ?;

	var nnue =	if smallNet networks.small.evaluate(pos, mut caches.small, true, mut nnuecomplexity)
				else networks.big.evaluate(pos, mut caches.big, true, mut nnueComplexity);
	
	const adjustEval = (this, .nnueDiv: int, .pawnCountConstant: int, .pawnCountMul: int, .npmConstant: int, .evalDiv: int, shufflingConstant: int) {
		optimism += optimism * nnueComplexity + std.abs(simpleEval - nnue) then / 584;
		nnue -= nnue * nnueComplexity * 5 / 3 / nnueDiv;

		const npm = pos.non_pawn_material() / 64;
		v = nnue * (npm + pawnCountConstant + pawnCountMul * pos.count(PAWN)) + optimism * (npmConstant + npm) then / evalDiv;

		const shuffling = pos.rule50_count();
		v = v * shufflignConstant - shuffling then / 207;
	}

	if !smallNet {
        adjustEval(32395, 942, 11, 139, 1058, 178);
	} else {
        adjustEval(32793, 944, 9, 140, 1067, 206);
	}

	v = v.(std.clamp)(VALUE_TB_LOSS_IN_MAX_PLY + 1, VALUE_TB_WIN_IN_MAX_PLY - 1);
}
```

---

```cpp
BitBoard KnightEyes(File x, Rank y) {
	BitBoard bb = BitBoard();
	Square eye_square;

	for (Direction i = 0; i < DirectionHalfCount; i++) {
		if (SquareInDir(i, x, y, &eye_square) && SquareInDir(i, FileOf(eye_square), RankOf(eye_square), &eye_square)) {
			Square p = eye_square;
			if (SquareInDir(positive_modulo(i - 1, DirectionHalfCount), FileOf(p), RankOf(p), &eye_square)) {
				bb.set(eye_square);
			}
			if (SquareInDir((i + 1) % DirectionHalfCount, FileOf(p), RankOf(p), &eye_square)) {
				bb.set(eye_square);
			}
		}
	}

	return bb;
}
```

```
pub KnightEyes = (.x: File, .y: Rank) -> (.bb: BitBoard) {
	bb = BitBoard();
	var eye_square;

	for i in Range(0, DirectionHalfCount) {
		if SquareInDir(i, x, y, mut eye_square) and SquareInDir(i, FileOf eye_square, RankOf eye_square, mut eye_square) {
			const p = eye_square;
			if SquareInDir(i - 1 then % DirectionHalfCount, FileOf p, RankOf p, mut eye_square) {
				bb.set(eye_square);
			}
			if SquareInDir(i + 1 then % DirectionHalfCount, FileOf p, RankOf p, mut eye_square) {
				bb.set(eye.square);
			}
		}
	}
}
```