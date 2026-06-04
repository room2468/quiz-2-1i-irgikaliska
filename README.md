# OS Quiz 2 — Bash Programming, Memory & File Management

This quiz covers Bash scripting (Chapter 7), memory management (Chapter 8), and file/user management (Chapter 9).

Each problem is a bash script that reads from **stdin** and writes to **stdout**. Replace the `echo "TODO"` line with your implementation. Do **not** change the output format.

Total score: **100 points**

| Problem | Difficulty | Points |
|---------|-----------|--------|
| 1 — Name Formatter | Easy | 20 pts (4 × 5) |
| 2 — Memory Checker | Easy-Medium | 20 pts (4 × 5) |
| 3 — File Classifier | Medium | 28 pts (4 × 7) |
| 4 — Disk Reporter | Medium | 32 pts (4 × 8) |

---

## Problem 1 — Name Formatter (20 pts)

**File:** `problem1/formatter`

Read a full name (first and last) from stdin. Output it formatted as `LASTNAME, Firstname` — last name in ALL CAPS, first name in Title Case.

**Example:**
```
$ echo "budi santoso" | ./problem1/formatter
SANTOSO, Budi
```

**Hints:**
- Use bash word splitting: `read -r first last`
- Use parameter expansion: `${var^^}` (uppercase), `${var^}` (capitalize first letter)

---

## Problem 2 — Memory Checker (20 pts, Easy-Medium)

**File:** `problem2/memory-checker`

Read two lines from stdin: total RAM in MB and used RAM in MB. Output the free MB, usage percentage, and a status based on usage:
- `Normal` if usage is below 70%
- `Warning` if usage is 70%–89%
- `Critical` if usage is 90% or above

**Example:**
```
$ printf "8000\n2000\n" | ./problem2/memory-checker
Free: 6000 MB
Usage: 25%
Status: Normal
```

**Hints:**
- Use `$(( total - used ))` to calculate free
- Use `$(( used * 100 / total ))` to calculate percentage
- Use `if (( usage >= 90 ))` for the status check

> A script `generate-memory-data` is available in the `problem2/` directory to produce real input data from your system. Figure out how to run it and pipe its output into your script.

---

## Problem 3 — File Classifier (28 pts, Medium)

**File:** `problem3/file-classifier`

Read a list of filenames from stdin (one per line). Count them by type and report:
- Shell scripts ending in `.sh`
- Log files ending in `.log`
- Config files ending in `.conf`
- Everything else as `Others`

**Example:**
```
$ printf "deploy.sh\nerror.log\nnginx.conf\nreadme.txt\n" | ./problem3/file-classifier
Scripts (.sh): 1
Logs (.log): 1
Configs (.conf): 1
Others: 1
```

**Hints:**
- Use a `while IFS= read -r filename` loop to read each line
- Use a `case "$filename" in` statement with wildcard patterns like `*.sh)`
- Use `(( scripts++ ))` to increment a counter

> A script `generate-file-list` is available in the `problem3/` directory to list real files from your system. Figure out how to run it and pipe its output into your script.

---

## Problem 4 — Disk Reporter (32 pts, Medium)

**File:** `problem4/disk-reporter`

Read lines from stdin where each line has a username and their disk usage in MB (e.g., `alice 1200`). Report:
- Total disk usage across all users
- The user with the highest usage (and their size)
- How many users are using more than 1000 MB

**Example:**
```
$ printf "alice 1200\nbob 450\ncharlie 2800\n" | ./problem4/disk-reporter
Total usage: 4450 MB
Highest user: charlie (2800 MB)
Users over 1000 MB: 2
```

**Hints:**
- Use `read -r username size <<< "$line"` to split each line into two variables
- Use `(( total += size ))` to accumulate the total
- Use `if (( size > highest_size ))` to track the highest user

> A script `generate-disk-usage` is available in the `problem4/` directory to collect real disk usage data from your system. Figure out how to run it and pipe its output into your script.
