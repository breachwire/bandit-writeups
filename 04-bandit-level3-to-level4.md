# OverTheWire: Bandit — Level 3 → Level 4

**Category:** Hidden files
**Difficulty:** Beginner

## Objective
Find a hidden file inside the `inhere` directory.

## Steps

```bash
cd inhere
ls -la
```
**Why `-a`:** hidden files (dotfiles) don't show with a plain `ls`. This directory contains one, e.g. `...Hiding-From-You`.

```bash
cat "...Hiding-From-You"
```
(exact filename varies by instance — use whatever `ls -la` actually shows you)

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
No issues — checking hidden files with `-a` is second nature at this point.

## Notes for next level

- [x] No quirks — checking hidden files with `-a` is already a reflex
- [x] No commands needed looking up

---
