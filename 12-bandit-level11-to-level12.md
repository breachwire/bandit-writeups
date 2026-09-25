# OverTheWire: Bandit — Level 11 → Level 12

**Category:** ROT13 cipher
**Difficulty:** Beginner–Intermediate

## Objective
`data.txt` contains the password shifted using ROT13 (each letter rotated 13 places through the alphabet).

## Steps

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

**Why `tr` and this exact mapping:** `tr` performs character-by-character substitution based on two matched sets. Mapping `A-Za-z` to `N-ZA-Mn-za-m` shifts every letter by 13 positions in both directions at once. ROT13 is a self-inverse cipher — applying it twice returns the original text, which is why the same command both encodes and decodes it.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Already understood the ROT13 concept (shift each letter 13 places) — checked the exact `tr` character-mapping syntax before running it, but the logic itself wasn't new.

## Notes for next level

- [x] Quirk: ROT13 is self-inverse, same command encodes and decodes
- [x] Looked up: exact `tr` character-mapping syntax for the shift

---
