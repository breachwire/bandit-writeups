# OverTheWire: Bandit — Level 10 → Level 11

**Category:** Base64 decoding
**Difficulty:** Beginner–Intermediate

## Objective
`data.txt` contains the password encoded in Base64.

## Steps

First attempt:
```bash
cat data.txt | base64 -decode
```
Result: `error: unexpected argument '-e' found` — this system's `base64` doesn't accept `-decode` as a long-form flag; it parsed it as short flags and choked on `-e`.

Second attempt:
```bash
cat data.txt | base64 - decode
```
Result: `base64: extra operand 'decode'` — splitting it into two words made `decode` look like a second file argument, not a flag at all.

Working command:
```bash
base64 -d data.txt
```
**Why this works:** the correct short flag is `-d` (single letter, single dash) — no `cat` needed either, since `base64` reads the file argument directly.

**Why Base64 is reversible with no key:** it's encoding, not encryption — it maps binary/text data into an ASCII-safe character set for safe transport, and `-d` just runs that mapping backward.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Guessed `-decode` as a long flag and got a cryptic parser error, then over-corrected by splitting it into two words, which just moved the error somewhere else. The actual flag was the simple one-letter `-d` the whole time — worth just checking `--help` first instead of guessing flag names.

## Notes for next level

- [x] Quirk: guessed `-decode` as a long flag, got "unexpected argument '-e'" — this box's `base64` doesn't parse long-form flags like GNU coreutils does
- [x] Looked up: correct short flag is `-d`, not the full word

---
