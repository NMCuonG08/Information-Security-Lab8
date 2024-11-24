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

## Mở file ảnh

```
eog original.bmp
```
![image](https://github.com/user-attachments/assets/c0df85e7-48fc-41ae-88c4-dbd77630c8fe)



## Thay thế 54 bytes header

```bash
dd if=header.bin of=origin-ecb-fixed.bmp bs=1 count=54
dd if=origin-ecb.bmp of=origin-ecb-fixed.bmp bs=1 skip=54 seek=54 conv=notrunc
```


## View 54 bytes 

```bash
xxd -l 54 original.bmp
```
