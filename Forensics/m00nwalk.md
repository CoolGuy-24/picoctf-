# m00nwalk

In this challenge, an audio file named `message` was provided which was a WAV file. Listening to the audio didn't give any clues.
So I used the tool `exiftool` to extract information about this file.

```
exiftool message.wav
ExifTool Version Number         : 12.40
File Name                       : message.wav
Directory                       : .
File Size                       : 11 MiB
File Modification Date/Time     : 2024:12:19 18:18:29+05:30
File Access Date/Time           : 2024:12:19 18:57:32+05:30
File Inode Change Date/Time     : 2024:12:19 18:49:12+05:30
File Permissions                : -rw-r--r--
File Type                       : WAV
File Type Extension             : wav
MIME Type                       : audio/x-wav
Encoding                        : Microsoft PCM
Num Channels                    : 1
Sample Rate                     : 48000
Avg Bytes Per Sec               : 96000
Bits Per Sample                 : 16
Duration                        : 0:01:55
```

This also didn't provide any information which could help me analyse this audio file. The clues were as follows:
```
How did pictures from the moon landing get sent back to Earth?
What is the CMU mascot?, that might help select a RX option
```
The answer to the first clue was in the [Website](https://www.scopeofwork.net/how-slow-scan-tv-shaped-the-moon/)
```
The crude videos from the moon were broadcast using slow-scan television, which influenced how we came to imagine the surface of the moon.
While we all know the moon isn’t literally a shaky video, it's hard to fully separate visual media of the moon from our internal concept of being on the moon, and I’ve been looking into the technologies that form that image.
Slow-scan TV (SSTV) is an image transmission method first used in the late 1950s, which is still used today. SSTV transmits image data over a frequency-modulated signal in the lower frequencies of the electromagnetic spectrum. In other words, it works just like FM radio, except instead of sound, it transmits images.
```
The answer to the second clue was `Scotty`

So with all this information I knew that the audio file was meant to transmit images, so all I needed was a SSTV decoder. I tried using the MSSTV decoder which was meant for windows but it was not giving me any output and I wa shaving trouble using it. So then I tried to clone a GitHub repository but that was also not working.

Finally an app named `Robot36` helped me decode the audio file message into an image. 

![image](https://github.com/user-attachments/assets/63168364-3daf-4c2a-b460-7379b3b5bfa3)

I downloaded this app on my phone and played the audio from my laptop. I set the setting to `Scottie1` and then soon an image started to form. The final image was:

![WhatsApp Image 2024-12-22 at 02 34 20_187559de](https://github.com/user-attachments/assets/b96be652-e431-4ea6-8bd0-d7c563cfca85)

This image clearly had the flag in it, all I had to do was wrap it in the flag format.

`FLAG:picoCTF{beep_boop_im_in_space}`
