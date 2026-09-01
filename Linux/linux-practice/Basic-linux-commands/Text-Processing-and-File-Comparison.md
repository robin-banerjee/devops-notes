# Text Processing and File Comparison

This section covers commands used for processing text content, filtering columns, sorting data, writing output with `tee`, and comparing files.

## Text Processing Commands

### `cut` Command

The `cut` command is used to cut sections from each line of files.

#### Example

```bash
$ cut -b 1 myfile.txt
l
l
l
l
l
l
l
l
l
l
```

```bash
$ cut -b 1-7 myfile.txt
line 1 
line 2 
line 3 
line 4 
line 5 
line 6 
line 7 
line 8 
line 9 
line 10
```

### `tee` Command

The `tee` command is used to read from standard input and write to both standard output and files simultaneously.

#### Example

```bash
$ echo "Hitesh sir is great at teaching" | tee chai-aur-code.txt
Hitesh sir is great at teaching
```

### `sort` Command

The `sort` command is used to sort the lines of text files. By default, it sorts alphabetically or ASCII-wise.

#### Example

```bash
$ sort chai-aur-code.txt
at 
great 
Hitesh 
is 
sir 
teaching
```

### `diff` Command

The `diff` command is used to compare files line by line.

#### Example

```bash
$ diff demofile.txt hardlink-file 
1c1
< Hi Bandhu
---
> hi bandhu... this is hardlink
```

### `wc` Command

The `wc` command prints newline, word, and byte counts for each file.

#### Example

```bash
$ wc chai-aur-code.txt demofile.txt myfile.txt 
6   6  37 chai-aur-code.txt
1   2  10 demofile.txt
10  90 342 myfile.txt
17  98 389 total
```

## Summary

- **`cut`**: Extracts specific bytes or character ranges from each line of a file.
- **`tee`**: Reads from standard input and writes to both standard output and files simultaneously.
- **`sort`**: Sorts the lines of text files. By default, it sorts alphabetically or ASCII-wise.
- **`diff`**: Compares files line by line.
- **`wc`**: Prints newline, word, and byte counts for each file.