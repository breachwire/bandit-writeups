# OverTheWire: Bandit — Level 9 → Level 10

**Category:** Binary/data file inspection — `strings` + `grep`
**Difficulty:** Beginner–Intermediate

## Objective
`data.txt` is mostly non-printable binary data. The password is one of the few human-readable strings inside it, marked by several `=` characters before it.

## Steps

First attempt:
```bash
cat data.txt | grep "==="
```
Result: `grep: (standard input): binary file matches`

**Why this happened:** `grep` detected that the input contains non-text (binary) bytes and, by default, refuses to print the actual matching content — it just reports that a match exists somewhere, as a safety behavior (dumping raw binary to a terminal can corrupt the display or trigger unwanted terminal escape sequences). Confirms the pattern exists, but doesn't show it.

Fixed approach:
```bash
strings data.txt | grep -E "==+"
```
**Flag breakdown:**
- `strings` — extracts only the printable-character runs from the binary file, sidestepping grep's binary-safety refusal entirely since the input to grep is now plain text
- `grep -E "==+"` — extended regex matching one or more consecutive `=` characters, since the exact count of `=` isn't known in advance

**Output had multiple decoy lines, not just one:**
```
cL0========== the
========== password
>========== is
R========== B0s2khmb***********************
```
The real password is the value after the equals-sign block on the *last* line — the other three lines are decoys forming a red-herring sentence ("... the / password / is / ...") to make you second-guess which line actually has it.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
The "binary file matches" message from plain `grep` threw me at first — didn't realize that meant "yes it's in there, but I won't show you." Also had to actually read all four matching lines instead of assuming the first hit was the answer — the decoys were clearly built to look like a taunting sentence pointing at the wrong lines.

## Notes for next level

- [x] Quirk: plain `grep` on the binary file said "binary file matches" instead of showing content — had to switch to `strings | grep` to actually see it
- [x] Quirk: multiple decoy lines matched the `==` pattern, forming a fake sentence — had to read all of them, not just take the first match

---
