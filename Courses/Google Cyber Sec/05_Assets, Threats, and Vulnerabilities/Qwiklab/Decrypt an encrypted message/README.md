# Decrypt an Encrypted Message
### Overview

In this lab, I practiced using Linux commands and encryption tools to decrypt hidden and encrypted files. I explored hidden files, solved a Caesar cipher, and used OpenSSL to decrypt an AES-encrypted file.

This exercise provided practical experience in cryptography, Linux command-line operations, and understanding symmetric encryption.

### Scenario

As a security analyst, all files in my home directory were encrypted. The task was to:

1. Locate hidden files containing instructions.

2. Decrypt a Caesar cipher to uncover the decryption command.

3. Use the revealed command to decrypt an AES-encrypted file and recover the hidden message.

This scenario demonstrated the importance of encryption in securing sensitive information and the practical use of Linux commands to handle encrypted data.

## Tasks and Commands
### Task 1: Explore Home Directory and Read Instructions

#### List all files:
```bash
ls
```

#### View contents of README.txt:
```bash
cat README.txt
```

#### Discovered a subdirectory caesar containing a hidden file.

### Task 2: Find Hidden File and Decrypt Caesar Cipher

#### Change into the caesar subdirectory:
```bash
cd caesar
```

#### List all files including hidden ones:
```bash
ls -a
```

#### View contents of hidden file .leftShift3:
```bash
cat .leftShift3
```

#### Decrypt the Caesar cipher (shift left by 3):
```bash
cat .leftShift3 | tr "d-za-cD-ZA-C" "a-zA-Z"
```

#### Revealed the OpenSSL command for decrypting the next file.

### Task 3: Decrypt AES-Encrypted File

#### Return to home directory:
```bash
cd ~
```

#### Use OpenSSL to decrypt the file:
```bash
openssl aes-256-cbc -pbkdf2 -a -d -in Q1.encrypted -out Q1.recovered -k ettubrute
```

#### View the recovered file:
```bash
cat Q1.recovered
```

#### Successfully decrypted the AES-encrypted file and read the hidden message.

### Key Learnings

1. Learned to identify and access hidden files using ls -a.

2. Practiced decrypting a Caesar cipher with the tr command.

3. Applied OpenSSL to decrypt AES-encrypted files.

4. Gained understanding of symmetric encryption (AES) and password-based decryption.

5. Learned how Linux command-line tools can assist in cryptography tasks.

### Conclusion

This lab improved my practical skills in Linux, encryption, and decryption. I now understand how hidden files, Caesar ciphers, and AES encryption work together to secure data, and how to recover sensitive information when provided with the correct tools and keys.
