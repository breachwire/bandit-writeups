# OverTheWire: Bandit — Level 2 → Level 3

**Category:** File handling / whitespace in filenames
**Difficulty:** Beginner

## Objective
Read a file whose name contains spaces — and, on this instance, leading and trailing double-dashes: `--spaces in this filename--`.

## Steps

```bash
ls -la
```
Shows the real filename exactly: `--spaces in this filename--`.

**What went wrong first:** a few plain-quoting guesses failed with `No such file or directory`, since they didn't account for the leading/trailing `--`. Once the real filename was quoted correctly, a different error appeared — `error: unexpected argument ... found` — meaning the file was found, but the leading `--` was being parsed as a command flag, not a filename.

```bash
cat ./"--spaces in this filename--"
```
**Why `./` fixes it:** prefixing with `./` forces the argument to be parsed as a relative path, not as a flag — the same fix as level 1, just needed here too because a filename starting with `-` (or `--`) is ambiguous to argument parsers in general, not just to `cat -`.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
A few quoting guesses failed before I noticed the actual filename had extra dashes I wasn't expecting — the `./` trick from level 1 fixed it once combined with quotes.

## Notes for next level

- [x] Quirk: actual filename had extra leading/trailing `--` not obvious from the level description; wrong guesses gave "No such file", the real filename (unquoted for `./`) gave "unexpected argument" instead
- [x] Looked up: nothing external, but had to reason through why the error type changed between attempts

---
