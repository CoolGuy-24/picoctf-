# HideToSee

In this challenge, there was an image `atbash.jpg` provided and the hint told to extract something from it.

This was the image. 

![image](https://github.com/user-attachments/assets/68c6645a-29ae-4d6a-bac7-a426c50c2f5d)

I used `exiftool` to analzye the image but there was nothing new.

```
coolguy24@Vedant-Laptop:~$ exiftool atbash.jpg
ExifTool Version Number         : 12.40
File Name                       : atbash.jpg
Directory                       : .
File Size                       : 50 KiB
File Modification Date/Time     : 2024:12:22 16:08:24+05:30
File Access Date/Time           : 2024:12:22 16:09:06+05:30
File Inode Change Date/Time     : 2024:12:22 16:09:06+05:30
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Image Width                     : 465
Image Height                    : 455
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 465x455
Megapixels                      : 0.212
```

Now since the hint told to extract, I tried using `steghide` and as expected the was something written, which got writen into `encrypted.txt` file.

```
coolguy24@Vedant-Laptop:~$ steghide extract -sf atbash.jpg
Enter passphrase:
wrote extracted data to "encrypted.txt".
```

The contents of the `encrypted.txt` file were:

```
krxlXGU{zgyzhs_xizxp_8z0uvwwx}
```

Now using the `atbash.jpg` image I decoded it to find the flag. 

`FLAG:picoCTF{atbash_crack_8a0feddc}`
