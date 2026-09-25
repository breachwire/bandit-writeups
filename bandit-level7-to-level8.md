# OverTheWire: Bandit — Level 7 → Level 8

**Category:** `grep` fundamentals
**Difficulty:** Beginner

## Objective
A file called `data.txt` contains many word/value pairs. The password sits next to a specific keyword.

## Steps

```bash
ls -la
```
Confirms `data.txt` exists, ~4MB.

```bash
cat data.txt | grep "millionth"
```
Worked first try — the line containing the keyword `millionth` also holds the password.

**Minor style note:** `cat data.txt | grep "millionth"` works, but `grep "millionth" data.txt` (no `cat`, no pipe) does the exact same thing with one less process spawned — this is the classic "useless use of cat" pattern. Not wrong, just worth knowing the shorter form exists.

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Fastest one so far, `grep` is something I already knew from dev work — first try, no errors.

## Notes for next level

- [x] No quirks — `grep` already familiar from dev work
- [x] No commands needed looking up

---
