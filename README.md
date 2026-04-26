# Grep Cheat Sheet

Essential grep commands for text searching and pattern matching in files.

---

## Table of Contents
- [Basic Commands](#basic-commands)
- [Common Options](#common-options)
- [Regular Expressions](#regular-expressions)
- [Extended Grep (egrep)](#extended-grep-egrep)
- [Fixed Grep (fgrep)](#fixed-grep-fgrep)
- [Recursive Searching](#recursive-searching)
- [Context Lines](#context-lines)
- [Multiple Patterns](#multiple-patterns)
- [Output Formatting](#output-formatting)
- [Practical Examples](#practical-examples)
- [Advanced Usage](#advanced-usage)

---

## Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `grep "pattern" file` | Search for pattern in file | `grep "error" log.txt` |
| `grep "pattern" file1 file2` | Search in multiple files | `grep "TODO" *.py` |
| `grep "pattern" *` | Search in all files in directory | `grep "config" *` |
| `cat file \| grep "pattern"` | Search in piped input | `cat log.txt \| grep "warning"` |
| `command \| grep "pattern"` | Filter command output | `ps aux \| grep "nginx"` |

## Common Options

| Option | Description | Example |
|--------|-------------|---------|
| `-i` | Case insensitive search | `grep -i "error" log.txt` |
| `-v` | Invert match (exclude lines) | `grep -v "debug" log.txt` |
| `-n` | Show line numbers | `grep -n "error" log.txt` |
| `-l` | Show only filenames with matches | `grep -l "TODO" *.py` |
| `-L` | Show only filenames without matches | `grep -L "TODO" *.py` |
| `-c` | Count matching lines | `grep -c "error" log.txt` |
| `-w` | Match whole words only | `grep -w "cat" file.txt` |
| `-x` | Match whole lines only | `grep -x "exact line" file.txt` |
| `-q` | Quiet mode (no output) | `grep -q "pattern" file && echo "found"` |
| `-s` | Suppress error messages | `grep -s "pattern" nonexistent.txt` |
| `-H` | Always print filename | `grep -H "pattern" file.txt` |
| `-h` | Never print filename | `grep -h "pattern" *.txt` |
| `--color` | Colorize matches | `grep --color "error" log.txt` |

## Regular Expressions

| Pattern | Description | Example |
|---------|-------------|---------|
| `.` | Any single character | `grep "a.b" file.txt` (matches "aab", "acb") |
| `*` | Zero or more of preceding | `grep "ab*" file.txt` (matches "a", "ab", "abb") |
| `^` | Start of line | `grep "^Error" log.txt` |
| `$` | End of line | `grep "done$" log.txt` |
| `[abc]` | Any character in brackets | `grep "[aeiou]" file.txt` |
| `[^abc]` | Any character not in brackets | `grep "[^0-9]" file.txt` |
| `[a-z]` | Character range | `grep "[a-zA-Z]" file.txt` |
| `\` | Escape special characters | `grep "\." file.txt` (literal dot) |
| `\<` | Start of word | `grep "\<cat" file.txt` |
| `\>` | End of word | `grep "cat\>" file.txt` |
| `\b` | Word boundary | `grep "\bcat\b" file.txt` |

## Extended Grep (egrep)

Extended regex patterns (use `grep -E` or `egrep`):

| Pattern | Description | Example |
|---------|-------------|---------|
| `+` | One or more of preceding | `grep -E "ab+" file.txt` |
| `?` | Zero or one of preceding | `grep -E "colou?r" file.txt` |
| `{n}` | Exactly n occurrences | `grep -E "[0-9]{3}" file.txt` |
| `{n,}` | n or more occurrences | `grep -E "[0-9]{3,}" file.txt` |
| `{n,m}` | Between n and m occurrences | `grep -E "[0-9]{3,5}" file.txt` |
| `\|` | OR operator | `grep -E "cat\|dog" file.txt` |
| `()` | Grouping | `grep -E "(cat\|dog)s?" file.txt` |

## Fixed Grep (fgrep)

Search for literal strings (use `grep -F` or `fgrep`):

| Command | Description | Example |
|---------|-------------|---------|
| `grep -F "string" file` | Literal string search | `grep -F ".*" file.txt` |
| `fgrep "string" file` | Same as grep -F | `fgrep "[ERROR]" log.txt` |
| `grep -F -f patterns.txt file` | Multiple literal patterns from file | `grep -F -f patterns.txt data.txt` |

## Recursive Searching

| Command | Description | Example |
|---------|-------------|---------|
| `grep -r "pattern" directory/` | Recursive search in directory | `grep -r "TODO" src/` |
| `grep -R "pattern" directory/` | Recursive with symlinks | `grep -R "config" /etc/` |
| `grep -r --include="*.py" "pattern" .` | Include specific file types | `grep -r --include="*.py" "import" .` |
| `grep -r --exclude="*.log" "pattern" .` | Exclude specific file types | `grep -r --exclude="*.log" "error" .` |
| `grep -r --exclude-dir=".git" "pattern" .` | Exclude directories | `grep -r --exclude-dir=".git" "TODO" .` |

## Context Lines

| Option | Description | Example |
|--------|-------------|---------|
| `-A n` | Show n lines after match | `grep -A 3 "error" log.txt` |
| `-B n` | Show n lines before match | `grep -B 2 "error" log.txt` |
| `-C n` | Show n lines before and after | `grep -C 2 "error" log.txt` |
| `--group-separator=SEP` | Separator between match groups | `grep -C 2 --group-separator="---" "error" log.txt` |

## Multiple Patterns

| Command | Description | Example |
|---------|-------------|---------|
| `grep -e "pat1" -e "pat2" file` | Multiple patterns | `grep -e "error" -e "warning" log.txt` |
| `grep -f patterns.txt file` | Patterns from file | `grep -f search_terms.txt data.txt` |
| `grep "pat1\|pat2" file` | OR with basic regex | `grep "error\|warning" log.txt` |
| `grep -E "pat1\|pat2" file` | OR with extended regex | `grep -E "cat\|dog" animals.txt` |

## Output Formatting

| Option | Description | Example |
|--------|-------------|---------|
| `-o` | Show only matching part | `grep -o "[0-9]\+" file.txt` |
| `-m n` | Stop after n matches | `grep -m 5 "pattern" file.txt` |
| `--line-buffered` | Force line buffering | `tail -f log.txt \| grep --line-buffered "error"` |
| `-T` | Make tabs line up | `grep -T "pattern" file.txt` |
| `-Z` | Null character after filename | `grep -lZ "pattern" * \| xargs -0 ls -l` |

## Practical Examples

### Log File Analysis
```bash
# Find all error messages
grep -i "error" /var/log/apache2/error.log

# Count different log levels
grep -c "ERROR" log.txt
grep -c "WARNING" log.txt
grep -c "INFO" log.txt

# Find recent errors with context
grep -A 5 -B 5 "$(date '+%Y-%m-%d')" /var/log/syslog | grep -i error

# Exclude debug messages
grep -v "DEBUG" application.log
```

### Source Code Search
```bash
# Find TODO comments in Python files
grep -r --include="*.py" "TODO\|FIXME\|HACK" .

# Find function definitions
grep -n "^def " *.py

# Find imports
grep -r "^import\|^from.*import" . --include="*.py"

# Find SQL queries
grep -r -i "select\|insert\|update\|delete" . --include="*.py"
```

### System Administration
```bash
# Find processes by name
ps aux | grep -v grep | grep nginx

# Find files modified today
find /path -type f -newermt "$(date '+%Y-%m-%d')" | grep -E "\.(log|conf)$"

# Check for failed login attempts
grep "Failed password" /var/log/auth.log

# Find large files in logs
find /var/log -name "*.log" -exec grep -l "size" {} \;
```

### Network and Security
```bash
# Find IP addresses
grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" access.log

# Find suspicious activities
grep -i "hack\|attack\|malware\|virus" /var/log/security.log

# Extract email addresses
grep -E -o "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# Find URLs
grep -E -o "https?://[^\s]+" file.txt
```

## Advanced Usage

### Combining with Other Commands
```bash
# Count unique occurrences
grep "pattern" file.txt | sort | uniq -c

# Find and replace (with sed)
grep -l "old_pattern" *.txt | xargs sed -i 's/old_pattern/new_pattern/g'

# Find files and show matches
find . -name "*.log" -exec grep -l "error" {} \;

# Use with xargs
grep -l "pattern" *.txt | xargs wc -l
```

### Performance Tips
```bash
# Use fixed strings for better performance
grep -F "literal_string" large_file.txt

# Limit search to specific file types
grep -r --include="*.txt" "pattern" /large/directory/

# Stop after first match
grep -m 1 "pattern" large_file.txt

# Use binary file detection
grep -I "pattern" * # Skip binary files
```

### Complex Patterns
```bash
# Match lines with specific word counts
grep -E "^(\S+\s+){5,10}\S*$" file.txt

# Find lines that don't contain any digits
grep -v "[0-9]" file.txt

# Match lines starting with capital letter
grep "^[A-Z]" file.txt

# Find empty lines
grep "^$" file.txt

# Find lines with only whitespace
grep "^\s*$" file.txt
```

---

## Resources
- [GNU Grep Manual](https://www.gnu.org/software/grep/manual/)
- [Regular Expressions Info](https://www.regular-expressions.info/)
- [POSIX Regex Documentation](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html)

---

## Author

🤖 casjay: [Github](https://github.com/casjay) 🤖

---
*Originally compiled from various sources. Contributions welcome!*
