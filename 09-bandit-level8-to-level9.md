# OverTheWire: Bandit — Level 8 → Level 9

**Category:** `sort` / `uniq`
**Difficulty:** Beginner

## Objective
`data.txt` contains many duplicate lines. The password is the one line that appears exactly once.

## Steps

```bash
cat data.txt | sort | uniq -u
```

**Why this order:** `uniq -u` only detects duplicates on *adjacent* lines, so the file has to be sorted first — otherwise identical lines scattered far apart wouldn't be caught. `-u` then prints only lines with no duplicate anywhere in the sorted output.

**Minor style note (same as level 7→8):** `cat data.txt | sort | uniq -u` works, but `sort data.txt | uniq -u` does the same thing without spawning `cat` at all — `sort` can read a file directly. Not wrong, just an extra process that isn't needed.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Easy, first try, no errors — already had the sort/uniq idea in mind from having done a similar filter earlier.

## Notes for next level

- [x] No quirks — had the sort/uniq idea in mind already
- [x] No commands needed looking up

---
