# OverTheWire: Bandit — Level 5 → Level 6

**Category:** `find` fundamentals
**Difficulty:** Beginner

## Objective
Somewhere inside `inhere` (20 subdirectories deep, `maybehere00`–`maybehere19`) there is exactly one file that is: human-readable, exactly 1033 bytes, and not executable. Everything else is a decoy.

## Steps

```bash
cd inhere
ls -la
```

First attempt:
```bash
find . -size 1033c ! executable
```
**Why it failed:** `find: paths must precede expression: 'executable'` — the `-executable` test needs its leading dash; without it, `find` reads `executable` as a bare word/path argument in the wrong position, not as a test at all. Also missing `-type f`, so it wasn't even scoped to regular files yet.

Fixed version:
```bash
find . -type f -size 1033c ! -executable -exec file {} \; | grep ASCII
```

**Flag breakdown:**
- `-type f` — only regular files
- `-size 1033c` — exact size in bytes (the `c` suffix matters — without it `find` assumes 512-byte blocks)
- `! -executable` — negation of the executable test; note the required dash before `executable`
- `-exec file {} \;` — runs `file` on every match so the type is actually known (same lesson carried over from level 4→5)
- `grep ASCII` — filters down to the one result that's actually readable text

```bash
cat ./maybehere07/.file2
```

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Missed the dash on `-executable` first try and got a syntax error, not a "no results" — good reminder that `find`'s test flags all need that leading `-`, it's not optional shorthand.

## Notes for next level

- [x] Quirk: forgot the dash on `-executable`, got a syntax error ("paths must precede expression") instead of empty results
- [x] Looked up: correct `find` test syntax — `-executable` needs the leading dash, and tests must come after `-type f`, not replace it

---
