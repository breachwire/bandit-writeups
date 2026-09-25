# OverTheWire: Bandit — Level 4 → Level 5

**Category:** File type identification
**Difficulty:** Beginner

## Objective
The `inhere` directory has ten files (`-file00` through `-file09`), only one of which is human-readable ASCII text — the rest are decoys.

## Steps

```bash
cd inhere
ls -la
```

First attempt — piping filenames straight into `grep`:
```bash
find . -type f | grep -E "ASCII text|Unicode text"
```
**Why this returned nothing:** `find` only outputs *filenames* (`-file00`, `-file01`, etc.) — none of them literally contain the text "ASCII text", so `grep` had nothing to match. The file-type description only exists in `file`'s output, not in the filename itself.

Fixed version:
```bash
find . -type f -exec file {} \; | grep -E "ASCII text|Unicode text"
```
**Flag breakdown:**
- `-exec file {} \;` — runs the `file` command on every result `find` returns, one at a time, substituting `{}` with each filename. This is the missing step — it's what actually generates the "ASCII text" description that `grep` can then filter for.
- `grep -E "ASCII text|Unicode text"` — filters the combined output down to whichever file(s) are flagged as readable text

```bash
cat ./-file07
```

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
First attempt piped filenames straight into grep and got nothing back — took a second to realize `find` alone doesn't know file *types*, only `file` does, so `-exec file {}` had to run first before grep had anything real to filter.

## Notes for next level

- [x] Quirk: piped `find` output straight into `grep "ASCII text"` first and got nothing — filenames don't contain that text, only `file`'s output does
- [x] Looked up: how to combine `find -exec file {}` with `grep` to filter by actual file type

---
