# OverTheWire: Bandit — Level 0 → Level 1

**Series:** Bandit (OverTheWire)
**Category:** Linux fundamentals / SSH / file enumeration
**Difficulty:** Beginner

---

## Objective

Log in to `bandit0` over SSH, locate the password for the next level, and use it to authenticate as `bandit1`. This level tests basic SSH usage and file-reading commands — the entry point for every level after it.

## Environment

| Item | Value |
|---|---|
| Host | `bandit.labs.overthewire.org` |
| Port | `2220` |
| Starting user | `bandit0` |
| Starting password | `bandit0` (published on the Bandit level-0 page) |

## Recon

Before touching a target, I check what's actually reachable rather than assuming defaults still apply.

```bash
nc -zv bandit.labs.overthewire.org 2220
```

**Why:** confirms the SSH service is up on the non-standard port before spending time debugging an auth issue that's actually a connectivity issue. Habit carried over from external recon on real engagements — don't assume, verify.

## Step 1 — Authenticate as bandit0

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**Flag breakdown:**
- `ssh` — initiates an encrypted remote shell session
- `bandit0@...` — user@host syntax
- `-p 2220` — non-default SSH port; without this the connection attempt goes to port 22 and times out

Password when prompted: `bandit0`

## Step 2 — Enumerate the home directory

```bash
ls -la
```

**Why `-la` and not just `ls`:** `-a` shows dotfiles (hidden files are a common place for secrets/configs to hide — worth building the reflex now), `-l` gives permissions and ownership, which matters later when levels involve permission-based privilege escalation.

Expected output should show a `readme` file.

## Step 3 — Read the file

```bash
cat readme
```

**Result:**
```
[REDACTED — per OverTheWire's request not to publish level solutions]
```

The file contained a single string used as the bandit1 password — not reproduced here, but the method above is enough for anyone to get their own.

## Step 4 — Authenticate as bandit1

```bash
exit
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Use the password retrieved in Step 3.

## Verification

```bash
whoami
# expected: bandit1
```

## Lesson / Takeaway
Easy, nothing suspicious — SSH login and reading a file, straightforward from the start.

## Notes for next level

- [x] Minor typo — typed `cat redme` before catching the correct spelling, no real issue
- [x] No commands needed looking up

---
