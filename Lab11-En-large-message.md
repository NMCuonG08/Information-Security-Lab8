
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


















