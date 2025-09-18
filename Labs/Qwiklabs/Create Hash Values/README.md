# File Hashing and Comparison
### Overview

In this lab, I learned how to generate hash values for files and compare them to verify file integrity. Using SHA256 hashing and comparison tools in Linux, I practiced detecting even the smallest differences between files.

This exercise provided hands-on experience with hashing, an essential security control for ensuring data integrity and detecting tampering.

### Scenario

As a security analyst, I needed to investigate whether two files, file1.txt and file2.txt, were identical. Even though the contents appeared similar, hashes provide a reliable way to detect changes.

The lab involved working with the following files:

1. file1.txt – Original test file (EICAR test string)

2. file2.txt – Similar to file1.txt but contained extra characters

## Tasks and Commands
### Task 1: Display File Contents

#### Display contents of file1.txt and file2.txt:
```bash
cat file1.txt
cat file2.txt
```

#### Output:

#### file1.txt:
#### X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*

#### file2.txt:
#### X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*
#### 9sxa5Yq20R


#### ⚠️ Although the files appear similar, file2.txt has extra characters.

### Task 2: Generate SHA256 Hashes

#### Generate hashes for both files:
```bash
sha256sum file1.txt
sha256sum file2.txt
```

#### Output:

#### file1.txt -> 131f95c51cc819465fa1797f6ccacf9d494aaaff46fa3eac73ae63ffbdfd8267
#### file2.txt -> 2558ba9a4cad1e69804ce03aa2a029526179a91a5e38cb723320e83af9ca017b


####  The hashes are completely different, confirming the files are not identical.

### Task 3: Save Hashes to Files

Write the hash values to separate files:

#### sha256sum file1.txt >> file1hash
#### sha256sum file2.txt >> file2hash

### Task 4: Compare Hash Files

#### Compare the two hash files using cmp:
```bash
cmp file1hash file2hash
```

#### Output:

#### file1hash file2hash differ: char 1, line 1


The first character differs, indicating the hash values are not the same.

### Key Learnings

1. Learned to generate SHA256 hashes for files using sha256sum.

2. Even small differences in files produce completely different hash values.

3. Used cmp to compare hash files and detect changes.

4. Hashing is a critical security technique to ensure data integrity and detect tampering.

### Conclusion

This lab reinforced the importance of hashing as a security control. By generating and comparing hashes, I learned to identify changes in files quickly and reliably, even when the files appear visually identical.
