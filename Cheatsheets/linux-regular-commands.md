# Linux Intermediate Commands Cheat Sheet

## File & Directory Search

```bash
find . -name "*.log"          # Find all .log files
find . -type d                # Find directories
find . -type f                # Find files
find . -size +10M             # Find files larger than 10 MB
```

---

## Search Text

```bash
grep "ERROR" security.log     # Search for ERROR
grep -i "error" security.log  # Case-insensitive search
grep -c "ERROR" security.log  # Count matching lines
history | grep ssh            # Search command history
```

---

## View Files

```bash
cat file.txt                  # Display entire file
less file.txt                 # View large files
head file.txt                 # First 10 lines
head -5 file.txt              # First 5 lines
tail file.txt                 # Last 10 lines
tail -5 file.txt              # Last 5 lines
tail -f file.txt              # Follow file in real time
```

---

## Hashing

```bash
sha256sum file.txt            # Generate SHA-256 hash
```

---

## Pipes

```bash
ip a | grep inet
grep "ERROR" security.log | wc -l
history | grep chmod
```

---

## Redirection

```bash
command > output.txt          # Overwrite output
command >> output.txt         # Append output
command 2> errors.txt         # Redirect errors
command > output.txt 2> errors.txt
command > all.txt 2>&1        # Redirect stdout & stderr
```

---

## Tee

```bash
command | tee output.txt      # Display and save output
```

---

## Count

```bash
wc file.txt                   # Lines, words, bytes
wc -l file.txt                # Count lines
wc -w file.txt                # Count words
wc -c file.txt                # Count bytes
```

---

## Links

```bash
ln file.txt file-hard         # Create hard link
ln -s file.txt file-link      # Create symbolic link
ls -li                        # View inode numbers
```

---

## Reports

```bash
pwd                           # Current directory
date                          # Current date & time
touch report.txt              # Create empty file
echo "Text" > file.txt        # Write text
echo "Text" >> file.txt       # Append text
```

---

## Useful Shortcuts

```text
Ctrl + R    Reverse search command history
!!          Repeat previous command
!$          Last argument from previous command
Tab         Auto-complete commands/files
```

---

## Quick Reminder

| Task | Command |
|------|---------|
| Find files | `find` |
| Search inside files | `grep` |
| Read large files | `less` |
| View first lines | `head` |
| View last lines | `tail` |
| Monitor logs | `tail -f` |
| Count | `wc` |
| Generate hash | `sha256sum` |
| Save output | `>` |
| Append output | `>>` |
| Redirect errors | `2>` |
| Display & save output | `tee` |
| Hard link | `ln` |
| Symbolic link | `ln -s` |
