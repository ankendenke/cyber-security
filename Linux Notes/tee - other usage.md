# Linux tee Command Tutorial
The `tee` command is a powerful utility in Linux that reads from standard input and writes to both standard output and one or more files simultaneously. Think of it like a "T" shaped pipe fitting in plumbing, where the input splits into two directions.

## Basic Usage

### 1. Simple Output Redirection
```bash
echo "Hello, World!" | tee output.txt
```
This command:
- Displays "Hello, World!" on the screen
- Simultaneously saves it to output.txt

### 2. Appending to Files
By default, `tee` overwrites files. Use the `-a` flag to append:
```bash
echo "First line" | tee file.txt
echo "Second line" | tee -a file.txt
```

## Intermediate Usage

### 3. Writing to Multiple Files
```bash
echo "Same content" | tee file1.txt file2.txt file3.txt
```

### 4. Combining with Other Commands
```bash
# Save command output while viewing it
ls -l | tee directory_listing.txt

# Save system information
uname -a | tee system_info.txt
```

### 5. Using with sudo
`tee` is often used to write to files that require root permissions:
```bash
echo "new configuration" | sudo tee /etc/some_config_file
```

## Advanced Usage

### 6. Using Process Substitution
```bash
echo "test" | tee >(grep "test" > filtered.txt) >(wc -l > line_count.txt) > original.txt
```

### 7. Creating Logs while Processing
```bash
# Log all steps of a pipeline
command1 | tee step1.log | command2 | tee step2.log | command3 | tee final.log
```

### 8. Suppressing Standard Output
Use the `-p` flag to ignore interrupts:
```bash
echo "silent write" | tee -p output.txt > /dev/null
```

### 9. Binary Mode
When dealing with binary data, use `--binary` or `-b`:
```bash
binary_command | tee --binary output.bin
```

### 10. Error Handling
Combining with error redirection:
```bash
(command 2>&1) | tee output.log
```

## Practical Examples

### Creating Backup Files
```bash
# Create a backup while editing
cat original.txt | tee original.txt.backup | editor

# Create timestamped backups
cat file.txt | tee file_$(date +%Y%m%d_%H%M%S).backup
```

### Logging Installation Processes
```bash
# Save installation logs while monitoring
./install.sh 2>&1 | tee installation_log.txt
```

### Monitoring and Logging System Stats
```bash
# Monitor system stats while logging
top -b -n 1 | tee system_stats.txt
```

## Tips and Best Practices

1. **Always use sudo with tee** instead of direct redirection when writing to protected files:
   ```bash
   # Correct:
   echo "content" | sudo tee /etc/protected_file
   # Wrong:
   sudo echo "content" > /etc/protected_file  # This won't work
   ```

2. **Consider using `-a` flag** when you want to preserve existing file content

3. **Use process substitution** for complex pipelines where you need to branch the output

4. **Remember binary mode** when dealing with non-text files

## Common Pitfalls

1. Forgetting that `tee` overwrites files by default
2. Not using sudo with `tee` when writing to protected files
3. Forgetting to quote strings with spaces when using echo with tee
4. Not considering character encoding when dealing with text files

## Advanced Tips for Scripts

When using `tee` in scripts, you can make it more robust:

```bash
# Ensure atomic writes
echo "content" | tee atomic.txt.tmp && mv atomic.txt.tmp atomic.txt

# Handle errors
if ! echo "content" | tee output.txt; then
    echo "Failed to write to file" >&2
    exit 1
fi
```