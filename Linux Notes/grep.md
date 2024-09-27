The `grep` command in [[Linux]] is a powerful tool used for searching and manipulating text patterns within files.

***Syntax***
The basic syntax of a grep command is as follow
```
grep [options] pattern [files]
```

***Options***

| Options | Description                                                                                     |
| ------- | ----------------------------------------------------------------------------------------------- |
| -c      | This prints only a count of the lines that match a pattern                                      |
| -h      | Display the matched lines, but do not display the filenames.                                    |
| –i      | Ignores, case for matching                                                                      |
| -l      | Displays list of a filenames only.                                                              |
| -n      | Display the matched lines and their line numbers.                                               |
| -v      | This prints out all the lines that do not matches the pattern                                   |
| -e expr | Specifies expression with this option. Can use multiple times.                                  |
| -f file | Takes patterns from file, one per line.                                                         |
| -E      | Treats pattern as an extended regular expression (ERE)                                          |
| -w      | Match whole word                                                                                |
| -o      | Print only the matched parts of a matching line, with each such part on a separate output line. |
| -A n    | Prints searched line and nlines after the result.                                               |
| -B n    | Prints searched line and n line before the result.                                              |
| -C n    | Prints searched line and n lines after before the result.                                       |

***Sample Commands***
Let say we have this below text in a file called geekfile.txt:
```
unix is great os. unix was developed in Bell labs.

learn operating system.

Unix linux which one you choose.

uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```
- Case insensitive search
```
grep -i "uNix" geekfile.txt
```
Output
```
unix is great os. unix was developed in Bell labs.
Unix linux which one you choose.
uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```
- Displaying the Count of Number of Matches Using grep
```
grep -c "unix" *
```
- Checking for the Whole Words in a File Using grep
```
grep -w "unix" geekfile.txt
```
Output
```
medtraore@medtraore-msi:~$ grep -w "unix" geekfile.txt
unix is great os. unix was developed in Bell labs.
uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```
- Displaying only the matched pattern Using grep
```
grep -o "unix" geekfile.txt
```
- Show Line Number While Displaying the Output Using grep -n
```
grep -n "unix" geekfile.txt
```
Output
```
medtraore@medtraore-msi:~$ grep -n "unix" geekfile.txt
1:unix is great os. unix was developed in Bell labs.
7:uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```
-  Inverting the Pattern Match Using grep
You can display the lines that are not matched with the specified search string pattern using the -v option.
```
grep -v "unix" geekfile.txt
```
Output
```
 grep -v "unix" geekfile.txt

learn operating system.

Unix linux which one you choose.
```
- Matching the Lines that Start with a String Using grep

```
 grep "^unix" geekfile.txt
unix is great os. unix was developed in Bell labs.
```
- Matching the Lines that End with a String Using grep
