## Code

```bash
openssl aes-128-cbc -e -in plain.txt -out aes128-cbc.enc -K 00112233445566778899aabbccddeeff -i v 010203040506070809aabbccddeeff00
```

```bash
openssl aes-128-cbc -d -in aes128-cbc.enc -out res.txt -K 00112233445566778899aabbccddeeff -iv 010203040506070809aabbccddeeff00
```

![image](https://github.com/user-attachments/assets/3b0b29f4-499b-4849-83d2-4547a41e5c00)


```bash
cp /mnt/c/WSL/original.bmp .
```

```
eog original.bmp
```
![image](https://github.com/user-attachments/assets/c0df85e7-48fc-41ae-88c4-dbd77630c8fe)

```bash
 dd if=original.bmp of=origin-ecb.bmp bs=54 seek=1 conv=notrunc
```
