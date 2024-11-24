
## Xóa toàn bộ file trong thư mục

```bash
rm -rf *
```


## Code

```bash
openssl aes-128-cbc -e -in plain.txt -out aes128-cbc.enc -K 00112233445566778899aabbccddeeff -i v 010203040506070809aabbccddeeff00
```

```bash
openssl aes-128-cbc -d -in aes128-cbc.enc -out res.txt -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```

![image](https://github.com/user-attachments/assets/3b0b29f4-499b-4849-83d2-4547a41e5c00)



# Mã hóa ảnh

```bash
openssl aes-128-ecb -e -in origin.bmp -out origin-ecb.bmp -K 00112233445566778899aabbccddeeff
```
```bash
openssl aes-128-cbc -e -in origin.bmp -out origin-cbc.bmp -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```
## Copy ảnh từ ngoài vào thư mục

```bash
cp /mnt/c/WSL/original.bmp .
```

## Mở file ảnh

```
eog original.bmp
```
![image](https://github.com/user-attachments/assets/c0df85e7-48fc-41ae-88c4-dbd77630c8fe)



## Thay thế 54 bytes header

```bash
dd if=original.bmp of=origin-ecb.bmp bs=1 count=54 conv=notrunc
```

- `if=origin.bmp`: Input file (original bitmap file).
- `of=origin-ecb-fixed.bmp`: Output file (fixed encrypted file).
- `bs=54` : Block size of 54 bytes (size of BMP header).
- `seek=1`: Skip the first 54 bytes in the output file (so the header is replaced).
- `conv=notrunc` : Ensure that no truncation happens during the copy.


## View 54 bytes 

```bash
xxd -l 54 original.bmp
```

What you might observe:

ECB Mode:

Since ECB mode encrypts each block independently, the image might still show some recognizable patterns or sections of the original image. However, the encryption will distort the colors and patterns, making it hard to derive exact details. If there are large uniform areas in the image (e.g., a solid color), those may still be visible in the encrypted image.

CBC Mode:
In CBC mode, each block depends on the previous one, and the image will likely appear as a random noise or distorted image. Even if the header is correctly replaced, the pixel data will not be recognizable and will look entirely scrambled.

Can you derive any useful information about the original picture?

In ECB mode, due to its block-by-block encryption nature, the image may still retain some structural patterns. However, the image will be largely unreadable, and any patterns you see will not represent meaningful data from the original image.
In CBC mode, since the encryption mixes each block with the previous one, the resulting encrypted image will look like random noise. Even if you replace the header, the content will be indecipherable.

Conclusion:

ECB tends to be more vulnerable to patterns, which could allow some form of information leakage, but in this case, it won't give you back a useful image.
CBC, on the other hand, makes the encrypted image much harder to reverse-engineer, providing better security but rendering the image completely unrecognizable without decryption.


![image](https://github.com/user-attachments/assets/6d2f1990-fe56-43a4-832d-c2c5771c4208)  ![image](https://github.com/user-attachments/assets/7f2776fd-4976-4a80-8d5a-7e39b18d6937)

# 4.3 

```bash
echo "This is a simple text file. It contains more than 64 bytes for testing encryption." > test.txt
```

Encrypt with ECB:

```bash
openssl aes-128-ecb -e -in test.txt -out test-ecb.enc -K 00112233445566778899aabbccddeeff
```

Encrypt with CBC:

```bash
openssl aes-128-cbc -e -in test.txt -out test-cbc.enc -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```

Encrypt with CFB:


```bash
openssl aes-128-cfb -e -in test.txt -out test-cfb.enc -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```

Encrypt with OFB:
```bash
openssl aes-128-ofb -e -in test.txt -out test-ofb.enc -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```

- A single bit of the 5th byte in the encrypted file presumably got corrupted, you can achieve
this corruption using dd command.

```bash
dd if=test-ecb.enc of=test-ecb-corrupted.enc bs=1 seek=4 count=1 conv=notrunc iflag=fullblock
```

- decrypt

```bash
openssl aes-128-ecb -d -in test-ecb-corrupted.enc -out test-ecb-decrypted.txt -K 00112233445566778899aabbccddeeff
```

a. How much information can you recover by decrypting the corrupted file, if the encryption mode is ECB, CBC, CFB, or OFB, respectively?

Before doing the task, we can hypothesize:

ECB: Since ECB mode encrypts each block independently, the corruption of one byte in a block (e.g., 5th byte) will affect only that block. The rest of the data in the file should be decrypted correctly.

CBC: In CBC mode, the corruption of one byte will affect not only the corresponding block but also the next block during decryption. So, the corrupted byte will make the decrypted data of the current block unreadable, and the next block will also be corrupted.

CFB: In CFB, the corruption of one byte affects the decrypted output of the current byte and all subsequent bytes. The next bytes will be completely altered.

OFB: In OFB, the corruption of one byte will only affect the current byte being decrypted, but the following bytes will remain intact.

Expected Recovery after Decryption:

ECB: You can recover most of the file except for the block containing the corrupted byte. The rest of the file will be decrypted correctly.

CBC: You will lose the current block and the next one. After that, the decryption should proceed normally.

CFB: You will lose the current byte and all subsequent bytes in the corrupted segment.

OFB: You will lose just the corrupted byte, with no further impact on subsequent bytes.

b. Explanation of Why These Effects Occur

ECB: Since blocks are encrypted independently in ECB, corrupting one byte only affects the corresponding block, without cascading to the next blocks.


CBC: Since CBC chains the encryption of blocks, corrupting one byte affects the current block and propagates an error to the next block, making it unreadable.

CFB: In CFB, the encrypted data is XORed with the previous ciphertext block, so corrupting one byte affects not only the current byte but also all following bytes.

OFB: Since OFB uses a keystream and doesn't depend on the previous ciphertext block, the corruption only affects the current byte being decrypted.

c. Implications of These Differences

ECB is not ideal for security purposes because it allows pattern retention in the encrypted data, which could leak information, but it provides better resilience to single-byte corruption compared to the other modes.

CBC offers better security by chaining blocks, but it is sensitive to corruption. A single corrupted byte causes both the current and next blocks to be corrupted, making it harder to recover data after corruption.

CFB and OFB are both feedback-based modes, but CFB is more sensitive to corruption (as it affects multiple subsequent bytes). OFB, on the other hand, is better suited for error recovery since it doesn't propagate errors as much as CFB.

Conclusion

Encryption Mode Impacts: Each mode behaves differently in terms of error propagation and recovery. ECB is the least affected by bit corruption, while CBC, CFB, and OFB show increasing levels of error propagation depending on the mode.









