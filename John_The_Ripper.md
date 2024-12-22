# John The Ripper
## Overview
- [What is John](#what-is-john)
- [Concept of Hash](#concept-of-hash)
- [How to Install John](#how-to-install-john)
- [Types of Mode in John](#types-of-mode-in-john)
- [Usage](#usage)
- [Crack Using --Single](#crack-using---single)
- [Crack Using --wordlist](#crack-using---wordlist)
- [Rules in John](#rules-in-john)
- [Crack Using --incremental](#crack-using---incremental)
- [Crack Multiple Hashes Together](#crack-multiple-hashes-together)
- [Crack Shadow File](#crack-shadow-file)
- [Crack Zip File](#crack-zip-file)

## What is John
John the Ripper, or "John," is a password cracking tool used in Kali Linux. It's designed to test the strength of passwords by trying to guess them. It uses various methods:

- Dictionary Attack: Uses a list of common passwords.
- Brute Force Attack: Tries every possible character combination.
- Hybrid Attack: Combines dictionary and brute force methods.

John is free, open-source, and supports many types of password hashes, making it a versatile tool for improving security by identifying weak passwords.

## Concept of Hash
```
Password -> hashFunction(Password) -> Store
123 -> 202cb962ac59075b964b07152d234b70 -> Store
```
Hash:A hash is a unique, fixed-size string created from input data of any size using a mathematical function.<br>
points:

- Password Security: Systems never store passwords, only hashes of those passwords.

- Data Integrity: Hashes Confirm Data Unchanged Even the smallest adjustment in input results in an entirely unique hash.

- Hashes are athenticating passwords and store any sensitive data.
- Security: Hashes help protect sensitive information.

Because hashes are fast to compute and hard to reverse (or duplicate), they are fundamental to security and data integrity.

Hash Functions Example:-
`MD4, MD5, SHAI, SHA256, SHA512`
## How to Install John
```
apt-get install John
```

### Types of Mode in John
- Single Mode
- Wordlist Mode
- Incremental Mode
- External Mode


### Usage
#### For which format support john:
    
    joh --list=formats

### Basic Syntax
```
john [path/to/hashfile] [options] [Formate]
john hashfile.txt --single --formate=RAW-MD5
```


### Crack Using --Single
```
john --single [path/to/hashfile]
```
- Uses simple rules to try common password patterns.

### Crack Using --wordlist
```
john --wordlist=/path/to/wordlist.txt [path/to/hashfile]
```
- Tries passwords from a specified wordlist file.

### Rules in John

https://github.com/openwall/john/blob/bleeding-jumbo/doc/RULES

### Crack Using --incremental
```
john --incremental [path/to/hashfile]
```
- Uses brute force to try all possible combinations of characters.



### Crack Multiple Hashes Together
[Content for Crack Multiple Hashes Together]

### Crack Shadow File
[Content for Crack Shadow File]

### Crack Zip File
[Content for Crack Zip File]
