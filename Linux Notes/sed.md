sed (stream editor) is a powerful text processing tool in Unix and [[Linux]] systems. It's used for parsing and transforming text using a simple, compact programming language.

Basic sed Usage:

1. Simple substitution:
```bash
sed 's/old/new/' filename
```
This replaces the first occurrence of 'old' with 'new' on each line.

2. Global substitution:
```bash
sed 's/old/new/g' filename
```
The 'g' flag replaces all occurrences, not just the first.

3. In-place editing:
```bash
sed -i 's/old/new/g' filename
```
This modifies the file directly instead of outputting to stdout.

4. Using different delimiters:
```bash
sed 's|/usr/local/bin|/usr/bin|g' filename
```
Useful when your pattern contains forward slashes.

Intermediate sed Usage:

5. Multiple commands:
```bash
sed -e 's/old/new/' -e 's/foo/bar/' filename
```
This applies multiple substitutions.

6. Using address ranges:
```bash
sed '2,5s/old/new/' filename
```
This applies the substitution only to lines 2 through 5.

7. Using regular expressions:
```bash
sed '/^#/d' filename
```
This deletes all lines starting with '#'.

8. Appending and inserting lines:
```bash
sed '2a\New line' filename     # Append after line 2
sed '2i\New line' filename     # Insert before line 2
```

Advanced sed Usage:

9. Using sed variables and branching:
```bash
sed '
/pattern/ {
    s/old/new/
    b end_label
}
s/different/replacement/
:end_label
' filename
```
This demonstrates branching based on a pattern match.

10. Multiline pattern space:
```bash
sed '
N
s/\n/ /
' filename
```
This joins pairs of lines.

11. Hold space usage:
```bash
sed '
1h
1!H
$g
s/\n/,/g
' filename
```
This collects all lines and joins them with commas at the end.

12. Using sed for arithmetic:
```bash
echo "5" | sed 's/.*/ &+2 /' | bc
```
This adds 2 to the input number (requires bc).

Pro-level sed Usage:

13. Creating a sed script file:
Create a file named 'script.sed':
```sed
#!/bin/sed -f
s/old/new/g
/pattern/d
```
Make it executable and use it:
```bash
chmod +x script.sed
./script.sed filename
```

14. Using sed for parsing and data extraction:
```bash
sed -n 's/.*<title>\(.*\)<\/title>.*/\1/p' webpage.html
```
This extracts the title from an HTML file.

15. Using sed with awk for complex text processing:
```bash
sed 's/^[[:space:]]*//' file | awk '{sum += $1} END {print sum}'
```
This removes leading whitespace and sums the first column.

Remember, sed is very powerful but can be complex. It's often used in combination with other Unix tools like grep, awk, and regular bash commands for more sophisticated text processing tasks.