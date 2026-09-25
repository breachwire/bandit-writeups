# OverTheWire: Bandit — Level 6 → Level 7

**Category:** `find` across the filesystem + permission errors
**Difficulty:** Beginner

## Objective
The target file is no longer in your home directory — it's somewhere on the entire filesystem, owned by user `bandit7`, group `bandit6`, and exactly 33 bytes.

## Steps

First few attempts searched the wrong scope:
```bash
find . -type f -size 33c -user bandit7 -group bandit6
find . -type f -size 33c -user bandit7 -group bandit6 -exec file {} \;
find . -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
```
**Why these returned nothing (no error, just empty):** all three searched `.` — the current directory (bandit6's home) — but the target file isn't anywhere under there. `find` doesn't fail loudly when a search scope simply doesn't contain a match; it just returns nothing, which looks identical to "no file exists" even though the real issue is "wrong starting point."

Fixed version — search the whole filesystem instead of just the home directory:
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

**Why `/` instead of `.`:** `/` is the filesystem root, so this searches every directory on the box, not just your home folder — necessary once the file's location is unknown rather than assumed nearby.

**Why `2>/dev/null`:** searching from `/` as a low-privilege user means `find` tries to enter thousands of directories it doesn't have permission to read, and prints a `Permission denied` line for each one. `2>` redirects file descriptor 2 (stderr — error output) specifically, separate from normal results (stdout); sending it to `/dev/null` discards those errors so only the actual match prints, instead of it being buried in noise.

**Result of the search:**
```
/var/lib/dpkg/info/bandit7.password
```
Worth noting — this isn't a file someone hid on purpose in a challenge-specific spot; it's a real system path (`dpkg`'s package-info directory) being repurposed to store the password, which is itself a small lesson: sensitive data can end up in ordinary-looking system locations.

```bash
cat /var/lib/dpkg/info/bandit7.password
```

## Result
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

## Lesson / Takeaway
Kept searching `.` and getting silent empty results before realizing the file wasn't under my home directory at all — had to switch to searching from `/` and add `2>/dev/null` to cut through the permission-denied spam once nearly the whole filesystem was in scope.

## Notes for next level

- [x] Quirk: searched `.` (home dir) three times with no error and no result — silent empty output masked that the scope was wrong, not that the file didn't exist
- [x] Looked up/clarified: why `/` is needed for a filesystem-wide search, and what `2>/dev/null` actually redirects (stderr specifically, not all output)

---
