# tunn3l v1s10n

In this challenge, a file called `tunn3l v1s10n` was provided and the description said to extract a flag from it. 

Since the file didn't have a file extenstion, I couldn't figure out its format so I used the `file` command and got this output:

```
coolguy24@Vedant-Laptop:~$ file tunn3l_v1s10n
tunn3l_v1s10n: data
```
This was not much of a help and reading the file was also not of any help as it had a lot of unreadable characters. I decided to try and search for the flag inside this file using the `grep` command but to no avail.

```
coolguy24@Vedant-Laptop:~$ grep "picoCTF" tunn3l_v1s10n
coolguy24@Vedant-Laptop:~$
```

The following command revealed that the file was a binary file, so I started using binary file tools to analyze the file.

```
coolguy24@Vedant-Laptop:~$ file -i tunn3l_v1s10n
tunn3l_v1s10n: application/octet-stream; charset=binary
```

Using `binwalk` revealed the following information:

```
coolguy24@Vedant-Laptop:~$ binwalk tunn3l_v1s10n

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
33211         0x81BB          TROC filesystem, 1263425345 file entries
948694        0xE79D6         StuffIt Deluxe Segment (data): f:IK
```

Both of these did not make much sense to me and researching them online also gave me no answers. I then tried using another tool to analyse this file.
The `exiftool`.

```
coolguy24@Vedant-Laptop:~$ exiftool tunn3l_v1s10n
ExifTool Version Number         : 12.40
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.8 MiB
File Modification Date/Time     : 2024:12:08 15:31:34+05:30
File Access Date/Time           : 2024:12:19 15:12:37+05:30
File Inode Change Date/Time     : 2024:12:19 15:12:12+05:30
File Permissions                : -rw-r--r--
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347
```

This told me that the file was a `BMP` file. I tried opening the `bmp` files using various methods listed below but all failed.
-Using `feh`
-Using `xdg`
-Using `eog`

So then I decided to change the extension of the file and open it but that too failed.

![image](https://github.com/user-attachments/assets/5e9d904e-9314-4376-8ab8-9b191fe8fd59)

I then decided to view the hexadecimal code fo the bitmap file. I used `hexedit` for it.  

![image](https://github.com/user-attachments/assets/ff6de3e0-360e-464a-8fba-663f43241bbb)


Reading up on the file format `bmp` I came to know the structure of a `bmp` file. This wikipedia page provided me with all the information.
[BMP File Format](https://en.wikipedia.org/wiki/BMP_file_format)


So in the header section at the offset hex of `0xA` the value was `BA`. The offset hex `0xA` provides the offset value i.e the starting address, of the byte where the bitmap image data (pixel array) can be found.
The pixel array begins at offset value of `0x36` so I replace the `BA DO` with `36 00` 

The offset hex `0xE` should provide the size of the header which is fixxed at 40. And 40 in hex is `0x28` so replacing it with `28 00`.

![image](https://github.com/user-attachments/assets/d4bbdb5c-ba93-4b24-8054-5feb7df2ed3d)

Saving these changes and now opening the bitmap file we get the image, 

![image](https://github.com/user-attachments/assets/ebcffbda-fcdb-40a6-b7ba-c7cb3c04340a)

Now we do get a flag but that is not the actual flag. The image looks incomplete so I tried to see if there was something wrong with the image height or width. 

The image size formula is to multiply height and width (this will help you to know the total number of pixel) Multiply the result by bit depth (this will help you to get the total number of bits data) Divide the result by 8.
This gives the image length to be `1041012` instead of `2893400` which the exiftool gave.

So now reverse calculating the height of the image, we get it as `850.4997`. The height of the image is written in the `0x16` offset hex value.

This reads `32 01` and converting 850 into hex we get `0x352` which is `52 03` in little-endian format. Saving these changes we get the following image,

![image](https://github.com/user-attachments/assets/32f8dce8-ad0a-4d4d-b833-5c92f6cce50c)

`FLAG: picoCTF{qu1t3_a_v13w_2020}`
