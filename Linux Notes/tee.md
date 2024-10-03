The `tee` command in [[Linux]] is used to read from standard input (stdin) and write to both standard output (stdout) and one or more files simultaneously. This can be useful when you want to view output in the terminal while also saving it to a file.

Here's a step-by-step guide from beginner to advanced on how to use the `tee` command:

### 1. **Basic Usage of `tee`**

The basic syntax for the `tee` command is:

```bash
command | tee [filename]
```

- `command`: This is any command whose output you want to redirect.
- `filename`: The file where you want to save the output.

#### Example 1: Viewing and saving output at the same time

```bash
echo "Hello, World!" | tee output.txt
```

This will:
- Print "Hello, World!" in the terminal.
- Save "Hello, World!" to `output.txt`.

### 2. **Appending to a File with `tee -a`**

By default, `tee` overwrites the file's contents. If you want to append to the file (add to the end of the file without overwriting), use the `-a` option.

#### Example 2: Appending output to a file

```bash
echo "Another Line" | tee -a output.txt
```

This will:
- Print "Another Line" in the terminal.
- Add "Another Line" to the end of `output.txt` without overwriting its previous content.

### 3. **Writing to Multiple Files**

You can write to multiple files simultaneously by providing multiple file names after the `tee` command.

#### Example 3: Writing to multiple files

```bash
echo "Multi-file output" | tee file1.txt file2.txt
```

This will:
- Print "Multi-file output" in the terminal.
- Save the same output in both `file1.txt` and `file2.txt`.

### 4. **Combining with Other Commands**

The `tee` command is often used with other commands to capture the output of programs.

#### Example 4: Capturing `ls` output

```bash
ls -l | tee ls_output.txt
```

This will:
- List files in the directory using `ls -l`.
- Show the output in the terminal.
- Save the output to `ls_output.txt`.

### 5. **Suppressing Output to Terminal**

If you don’t want the output to be displayed in the terminal (only want to save it to a file), you can redirect the output to `/dev/null`.

#### Example 5: Suppressing terminal output

```bash
ls -l | tee ls_output.txt > /dev/null
```

This will:
- Save the output of `ls -l` to `ls_output.txt`.
- Suppress the terminal output (it won’t display in the terminal).

### 6. **Using `tee` with `sudo`**

Sometimes, you need to use `tee` with `sudo` to write to a file that requires elevated privileges.

#### Example 6: Writing to a protected file with sudo

```bash
echo "Protected content" | sudo tee /etc/protected_file.txt
```

This will:
- Prompt for your password because you're using `sudo`.
- Print "Protected content" in the terminal.
- Write "Protected content" to `/etc/protected_file.txt`.

Note: If you were to try `sudo echo "Protected content" > /etc/protected_file.txt`, you would get a permission denied error because the redirection happens before `sudo` is applied. `tee` solves this problem.

### 7. **Advanced Usage: Using `tee` with Command Substitution**

You can use `tee` with command substitution to store the output of a command while also logging it to a file.

#### Example 7: Storing command output in a variable and saving to a file

```bash
output=$(ls -l | tee ls_output.txt)
```

This will:
- Print the output of `ls -l` in the terminal.
- Save the output in `ls_output.txt`.
- Store the output in the `output` variable for further processing.

### 8. **Piping Multiple Commands with `tee`**

You can chain multiple commands together using pipes and `tee`. This can be useful for debugging or monitoring.

#### Example 8: Piping to multiple commands with `tee`

```bash
ls -l | tee ls_output.txt | grep ".txt"
```

This will:
- Show the output of `ls -l` in the terminal.
- Save the output of `ls -l` to `ls_output.txt`.
- Pipe the output to `grep` to filter and display only files that contain `.txt`.

### Summary of Common Options:
- `-a`: Append to the file instead of overwriting it.
- `-i`: Ignore interrupt signals.
- `-p`: Write to pipes without failing if any of them close.

### Conclusion

The `tee` command is versatile and handy for various scenarios, such as logging outputs, appending data to files, and capturing command outputs while still displaying them. As you become more familiar with pipes and redirects, you'll find more creative and advanced ways to use `tee` in your Linux workflows.