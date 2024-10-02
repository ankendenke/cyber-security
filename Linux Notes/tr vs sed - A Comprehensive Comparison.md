
[[Linux]]
## Quick Overview

### tr (translate)
- Simple character-based operations
- Works only with standard input (stdin)
- Performs character-by-character translations
- Cannot use regular expressions
- Cannot modify files in place

### sed (stream editor)
- Advanced pattern matching and text manipulation
- Can work with files directly
- Performs line-based operations
- Supports regular expressions
- Can modify files in place

## Detailed Comparison

### 1. Basic Functionality

#### tr
- Limited to:
  - Character translation
  - Character deletion
  - Character squeezing (removing repeating characters)

```bash
# Using tr
echo "hello world" | tr 'a-z' 'A-Z'      # Convert to uppercase
echo "hello  world" | tr -s ' '          # Squeeze spaces
echo "hello123" | tr -d '0-9'            # Delete numbers
```

#### sed
- Capable of:
  - Search and replace
  - Insertion and deletion of lines
  - Pattern matching with regex
  - Multiple operations in sequence
  - Complex text transformations

```bash
# Using sed
sed 's/hello/Hi/'                        # Simple replacement
sed '/pattern/d'                         # Delete lines matching pattern
sed '2i\New Line'                        # Insert line at position 2
sed '1,5p'                              # Print lines 1-5
```

### 2. Input/Output Handling

#### tr
```bash
# tr can only work with stdin
echo "input" | tr 'a-z' 'A-Z'           # Works
tr 'a-z' 'A-Z' file.txt                 # Won't work
cat file.txt | tr 'a-z' 'A-Z'           # Correct way
```

#### sed
```bash
# sed can work with both files and stdin
sed 's/old/new/' file.txt               # Works directly with file
echo "input" | sed 's/old/new/'         # Also works with stdin
sed -i 's/old/new/' file.txt            # Modify file in place
```

### 3. Pattern Matching

#### tr
```bash
# tr only matches single characters or character sets
echo "hello 123" | tr 'aeiou' '12345'    # Character-by-character replacement
echo "hello world" | tr '[:lower:]' '[:upper:]'  # Using character classes
```

#### sed
```bash
# sed supports complex pattern matching with regex
sed 's/[0-9]\{3\}-[0-9]\{2\}-[0-9]\{4\}/XXX-XX-XXXX/' # Match SSN pattern
sed '/^[A-Za-z].*:$/p'                  # Print lines ending with colon
sed '/pattern1/,/pattern2/d'            # Delete between two patterns
```

### 4. Common Use Cases

#### tr Use Cases
1. Simple character conversions:
```bash
# Convert Windows line endings to Unix
tr -d '\r' < windows.txt > unix.txt

# Create wordlist by removing punctuation
cat text.txt | tr -cd '[:alnum:]\n '
```

2. Basic data cleaning:
```bash
# Remove all non-printable characters
cat file.txt | tr -cd '[:print:]\n'

# Convert multiple spaces to single space
cat file.txt | tr -s ' '
```

#### sed Use Cases
1. Complex text manipulation:
```bash
# Add line numbers to file
sed = file.txt | sed 'N;s/\n/ /'

# Comment out lines matching pattern
sed '/pattern/s/^/#/' file.txt
```

2. Multiple operations:
```bash
# Multiple substitutions in one command
sed -e 's/old/new/' -e 's/foo/bar/' file.txt

# Complex pattern-based editing
sed '/pattern/{s/old/new/;s/foo/bar/}' file.txt
```

### 5. Performance Considerations

#### tr
- Faster for simple character translations
- Lower memory usage
- Better for processing large files with simple transformations

#### sed
- More overhead due to regex engine
- Higher memory usage for complex operations
- Better for complex text processing tasks

### 6. Practical Examples in System Administration

#### Using tr
```bash
# Clean up log files
cat logfile.txt | tr -cd '[:print:]\n' > clean_log.txt

# Generate random password
tr -dc 'A-Za-z0-9!@#$%^&*' < /dev/urandom | head -c 12
```

#### Using sed
```bash
# Comment out configuration lines
sed -i '/^SETTING/s/^/#/' config.txt

# Add timestamp to log entries
sed 's/^/[$(date)]: /' logfile.txt
```

## When to Use Which?

### Use tr when:
- You need simple character-based transformations
- Processing involves character-by-character operations
- Working with standard input streams
- Performance is critical for simple operations

### Use sed when:
- You need pattern matching with regex
- Working directly with files
- Performing complex text transformations
- Need to modify files in place
- Require line-based operations
- Need to perform multiple operations in sequence

## Combining Both Tools

Sometimes, using both tools together can be powerful:

```bash
# Clean and transform log files
cat logfile.txt | tr -s ' ' | sed 's/ERROR/*** ERROR ***/'

# Process configuration files
cat config.txt | tr -d '\r' | sed 's/^#.*//;/^$/d'
```