# OverTheWire: Bandit — Level 1 → Level 2

**Category:** File handling / shell argument parsing
**Difficulty:** Beginner

## Objective
Read a file whose name is a single dash (`-`), which the shell normally treats as a flag/stdin marker instead of a filename.

## Steps

```bash
ls -la
```
Home directory contains a file literally named `-`.

```bash
cat ./-
```
**Why `./-` and not `cat -`:** a bare `-` after `cat` is interpreted as "read from stdin," not "open the file named dash." Prefixing with `./` forces the shell to treat it as a relative path.

Alternative that works the same way:
```bash
cat < -
```

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Straightforward once I saw the `./` trick — no confusion, just knew what to do.

## Notes for next level

- [x] No quirks — knew the `./` trick already, no confusion
- [x] No commands needed looking up

---
