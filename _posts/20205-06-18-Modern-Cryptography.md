---
title: "Modern Cryptography"
description: ""
date: 2025-06-18 21h:00:00 -0000
categories:
  - Other
tags:
  - Programming
published: true
img_path: /assets/
---

Modern Cryptography
Mitch Hart
23 Jan
Introduction
This report analyses various encrypted texts using classical and modern cipher techniques. For each ciphertext, the process includes identifying the cipher, explaining the decryption process, providing plaintext and ciphertexts, and conducting frequency analysis where applicable. The study highlights systematic approaches and critical contextual reasoning to decrypt messages.

Morden Ciphers
XOR Encryption - Part 1
Ciphertext: 0F 14 01 00 16 59 25 04 05 0F 1F 0A 67 00 1E 04 58 1E 35 04 0D 15 58 18 23 00 1C 15 17 0B 34 4D 4C 00 16 1D 67 03 15 41 14 0C 29 02 04 15 11 14 22 41 00 08 1E 1C 67 08 02 41 0C 11 22 41 09 0F 0E 10 35 0E 02 12 58 16 21 41 2D 13 0C 11 32 13 4B 12 58 11 28 14 1F 04 58 11 26 05 4C 12 1D 0D 33 0D 09 05 58 10 29 15 03 41 19 59 34 15 09 00 1C 00 67 13 03 14 0C 10

Cipher Identification: The ciphertext is presented in hexadecimal format, a common encoding for XOR-encrypted text. The repeating nature of the ciphertext and the information of human-readable keys indicate that XOR encryption has been used with a repeating key.

Decryption Process: Initial conversion with the hexadecimal ciphertext was converted into binary to prepare for XOR operations. For example: • Hex 67 -> Binary: 01100111 A crib-dragging method was applied using common bigrams and trigrams, such as “the” and “and” along with the ASCII value of “ “ (space, 0x20) was XORed with sections of the ciphertext. Partial plaintext fragments began to emerge:



This XOR output produces the binary value of 01000111 which when converted back into ASCII, is a plain text character of uppercase ”G”. Repeating this process throughout the bulk of the ciphertext produces the letters “G”, “y” and “x”.


Given that these letters are plain English, and the key is 6 digits long the hypothesis is that the number of words with these letters in had narrowed down the search to some possibilities, exergy, oxygen, and galaxy. Given the context of the ciphers being related to Hitchhiker's Guide to the Galaxy and the capital G found, the next best thing to try is Galaxy as the passphrase. This was tested by XORing the ciphertext with a repeated key of Galaxy which verified its accuracy. Had this have not worked, continuing onto the next lines of text and repeating the brute force for common bigrams and trigrams “th”, “he”, “the” or “and”.

Key: “Galaxy” • Plaintext: See Appendix H Frequency Analysis: There is a strong peak around byte value 32 (hexadecimal 20). In ASCII, 20 represents a space character which suggests the plaintext is using a repeatable key and can be used this for our brute force.

Frequency Analysis:


Plaintext: Human beings are great adaptors, and by lunchtime life in the environs of Arthur's house had settled into a steady rout

XOR Encryption - Part 2
Ciphertext: 10 1D 34 15 20 06 2B 10 3D 63 1A 3C 50 23 00 33 19 2A 63 15 3C 04 74 1C 23 1C 34 26 16 79 07 3D 1B 2E 55 21 27 16 35 09 74 0B 2F 06 3A 31 13 3A 04 31 0B 66 18 21 2C 16 2A 50 35 01 22 7F 3D 37 13 2B 15 74 06 28 7F 3A 2C 52 2D 18 31 4F 35 1E 37 63 13 2A 50 3D 09 66 1D 37 33 1C 36 04 3D 15 23 11 6E 36 1C 2D 19 38 4F 35 1A 23 26 1D 37 15 74 0E 35 1E 2B 27 52 31 19 39 4F 31 1D 2F 37 52 31 15 74 18 27 06 6E 27 1D 30 1E 33 41 66 21 26

Cipher Identification: Like the above text, the ciphertext’s hexadecimal format and repeating patterns indicated XOR encryption. The space character appearing most frequent suggest the text is formatted in plaintext English. The length of the key (9 bytes) was given along with the text.

Decryption Process: The ciphertext was firstly converted from hexadecimal into binary for processing. The brute force key will be the space character as it’s the most common from the frequency analysis.


The next step is to XOR these and find the possible plain text characters.


Given that the only two plain text characters found were “C” and “p” the next step is to do this for the rest of the lines until a more letters are revealed. The result of all plain text characters is “C, p, C, T, Y, u, T, F, p, T, r, C, p, F, N, o, T, r, o, r, T, N, F”. This doesn’t appear to point to any obvious 9 letter words, so next is to look at crib dragging some common words through our text. Crib dragging is an attack against XOR encryption which involved guessing a potential word (the “crib”) and “dragged” along the ciphertext to find meaningful patterns. Common trigrams with spaces either side to get a 5-byte slide starting with “ the “ being the most common trigram does yield results starting from byte 73, “rYpTo” is found which does fit in the list of plain text characters found. Removing “r, Y, p, T, o” from the list of plain text characters is "C, C, u, F, C, F, N, N, F” or “C, u, F, N” without repeating characters. This reveals that since the found characters plus the remaining characters are equal to 9 bytes it is assumed the pass key is a combination of these characters, after some trial and error the key “CrYpToFuN” or “43 72 59 70 54 6f 46 75 4e” is found. 

Key: “CrYpToFuN” 

Frequency Analysis:


Plaintext: Sometimes he would get seized with oddly distracted moods and stare in to the sky as if hypnotized until someone asked him what he was doing. Th

Modes of Operation
Modes of operation are techniques used to secure data in block ciphers, transforming fixed-size blocks into variable-length ciphertexts suitable for different applications. These modes enable encryption algorithms to process data of various sizes, from stream data to large files. Two examples of modes of operation are OFB (Output Feedback Mode) and CTR (Counter Mode). OFB turns a block cipher into a stream cipher by encrypting an IV and using the output as a keystream, which is XORed with plaintext. A key strength of OFB is its error-tolerant nature, as errors in one ciphertext block affect only the corresponding plaintext block and don’t propagate. However, reusing the same IV and key combination results in keystream repetition, making it vulnerable to attacks like the known-plaintext attack. The need for unique IVs and the computational overhead contribute to slower performance.


CTR mode encrypts a counter combined with an IV to generate a keystream, which is XORed with plaintext. This mode is also error-tolerant, as errors don’t propagate. However, reusing the counter and IV combination leads to keystream reuse, compromising security. Its efficiency makes it faster than OFB, but like OFB, it requires careful management of the counter and IV.


RSA – Rivest–Shamir–Adleman
RSA is a public-key cryptographic algorithm that secures data using a pair of keys: a public key (encryption) and private key (decryption). It begins by generating two large random prime numbers, p and q, often 2048-bits as recommended by NIST, typically containing 617 decimal digits or up to 22048 – 1. Their product n (p * q = n) is used as the modulus for public and private keys, must be made public. The modulus n = p * q is used for Euler’s totient function φ(n) = (p – 1) (q – 1), which calculates the number of integers less than n that are coprime to n. A public exponent e is chosen, such that 1 < e < φ(n) and gcd(e, φ(n)) = 1. The private key d is computed using the extended Euclidean algorithm as the modular inverse of e mod φ(n), satisfying de = 1 mod (n). The modulus is used during encryption and decryption to secure communications. RSA’s longevity is due to its scalability; key lengths have increased from 512-bit to 2048-bit to counter growing computational power. However, quantum computing poses a threat as algorithms such as Shor’s could potentially break RSA prompting research into quantumresistant encryption.

RSA Exercise
>>> #Generating our two random 256-bit primes and assigning them to p and q.

 >>> p = getPrime(256) 

>>> q = getPrime(256)

>>> #Checking our primes have been assigned correctly. 

>>> p 

210608074735039491550872810453086239398857126642770758753348957193049423571953 

>>> q 

198494642376902393769619080464770796368899596583327740397722925106823146603961 

>>> #Computing n, n is the modulus used for both encryption and decryption. 

>>> n = p * q >>> #Confirming the value of 'n'. 

>>> n 

41804574476219596246099741429483274250381591391306029301292647859360843222993674989556864566015184962740951661018243063171721159433353417238899734078305833 

>>> #Setting the public exponent 'e' to 655537 or 0x10001, this gives us a strong number whilst maintaining efficiency of multiplications. 

>>> e = 65537 

>>> #Confirming the value of 'e'. 

>>> e

65537 

>>> #Euler's totient function which calculates the number of integers less than n that are coprime. 

>>> phin = (p-1) * (q-1) 

>>> #Confirming the value of 'phin'. 

>>> phin 

418045744762195962460997414294832742503815913913060293012926478593608432229326588683975262412986447085003380398247530644849506093420234535659986150 8129920 

>>> #Computing the Private Key 'd' where d is the modular inverse of e modulo phi(n). 

>>> d = modinv (e, phin)

>>> #Confirming the value of 'd'. 

>>> d 

21194754049183644726935259601102289600034013414695903620764618618841001842781897945008536558615179315088180313485904252671989035043727075227180731469713793 

>>> #Assigning our Public key to (e, n). 

>>> publicKey = (e, n) 

>>> #Confirming the value of publicKey. 

>>> publicKey (65537, 4180457447621959624609974142948327425038159139130602930129264785936084322299367498955686456601518496274095166101824306317172115943335341723889973407 8305833)

>>> #Assigning our Private key to (d, n). 

>>> privateKey = (d, n) 

>>> #Confirming the value of privateKey. 

>>> privateKey 

(211947540491836447269352596011022896000340134146959036207646186188410018427818979450085365586151793150881803134859042526719890350437270752271807314 69713793, 4180457447621959624609974142948327425038159139130602930129264785936084322299367498955686456601518496274095166101824306317172115943335341723889973407 8305833) 

>>> #Setting our plaintext message to the decimal conversion, Vogon = 371236237166. 

>>> plainText = 371236237166 

>>> #Confirming our plain text that has been converted to decimal, and hex is accurate. 

>>> hex(371236237166) '0x566f676f6e' 

>>> #Confirming the value of plainText. 

>>> plainText 371236237166 

>>> #Encrypting the plaintext message using our public key. 

>>> pow(plainText, e, n) 4180003960674110317638310198497378031773179943151004134099348138708835479498308581910880521765095822769096531686667687597313755661871958372470261960 8312956 

>>> #Assigning the encrypted data to the variable cipherText for decryption. 

>>> cipherText = 4180003960674110317638310198497378031773179943151004134099348138708835479498308581910880521765095822769096531686667687597313755661871958372470261960 8312956

>>> #Confirming the value of cipherText.

>>> cipherText 4180003960674110317638310198497378031773179943151004134099348138708835479498308581910880521765095822769096531686667687597313755661871958372470261960 8312956 

>>> #Decrypting the encrypted text of 'cipherText' back to decimal using our private key.

>>> pow(Ciphertext, d, n) 371236237166

Tools Used
Common bigrams and trigrams https://www3.nd.edu/~busiforc/handouts/cryptography/Letter%20Frequencies.html 

Converting ASCII, decimal and hexadecimal https://www.rapidtables.com/ 

Frequency Analysis https://crypto.soc.port.ac.uk/crypto/cryptoweb/freq.html 

Index of Coincidence https://crypto.soc.port.ac.uk/crypto/cryptoweb/ioc.html 

Substitution Cipher Tool https://webspace.maths.qmul.ac.uk/b.noohi/MTH6115/SubTool.html

Conclusion
This exploration of cryptography demonstrates how classical techniques laid the foundation for modern encryption methods. Whether solving substitution ciphers or decrypting XOR-encoded text, these techniques underline the importance of cryptographic systems in securing data.