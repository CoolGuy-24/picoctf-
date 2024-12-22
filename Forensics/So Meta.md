# So Meta

This challenge proved to be very easy. There was a file given with the name `pico_img` and it was `png` file. Opening it resulted in this image:

![pico_img](https://github.com/user-attachments/assets/7e1651e8-013a-475a-94db-3cbb48c1d5e6)

The hints mentioned that there is something to do with the metadata of the file. I opened the file in linux and used the command `exiftool` to analyze the file.

The artist name contained the flag.
```
coolguy24@Vedant-Laptop:~$ exiftool pico_img.png
ExifTool Version Number         : 12.40
File Name                       : pico_img.png
Directory                       : .
File Size                       : 106 KiB
File Modification Date/Time     : 2024:12:22 14:25:37+05:30
File Access Date/Time           : 2024:12:22 14:34:50+05:30
File Inode Change Date/Time     : 2024:12:22 14:26:58+05:30
File Permissions                : -rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Warning                         : [minor] Text/EXIF chunk(s) found after PNG IDAT (may be ignored by some readers)
Artist                          : picoCTF{s0_m3ta_eb36bf44}
Image Size                      : 600x600
Megapixels                      : 0.360
```

`FLAG:picoCTF{s0_m3ta_eb36bf44}`
