# WebNet0

This challenge had two files named `capture.pcap` and `picopico.key`. I have worked with a `pcap` file before so I knew that these files hold network traffic in them and a good tool to analzye them is Wireshark.

I opened the `capture.pcap` file in Wireshark.

![image](https://github.com/user-attachments/assets/5d2ad5e7-0f4d-44a9-8614-189fdfc91b73)

I was scrolling throught the streams and this where `PicoCTF` caught my eye so I clicked on it to view what it was.

![image](https://github.com/user-attachments/assets/1578305c-5cf5-4af6-b0e3-9fd0e1e77457)

I tried making sense of what it was and was inspecting the things written to make sense of it and figure out if this was a way to get the flag. 
I realised that this was just an indication of the challenge name and the other things were related to the host location etc.

I opened the `picopico.key` file and found out that this was had to private key.

![image](https://github.com/user-attachments/assets/b252936f-2190-4b3f-aa42-e9bad58e29ae)

Reading the hints which were
> Try using a tool like Wireshark.

> How can you decrypt the TLS stream?

I searched up how to decrypt a TLS stream in Wireshark using a private key and found out how to do it. [This](https://wiki.wireshark.org/TLS#tls-decryption) helped me with how to decrypt the TLS streams.

After adding the `picopico.key` file, there were new HTTP decrypted streams which were not present before.

![image](https://github.com/user-attachments/assets/8ac32ac5-c4b3-4401-9716-a8559724c40e)

I followed the TLS stream for the first new stream that is the number 31 stream and then there was the flag.

![image](https://github.com/user-attachments/assets/efc5de1e-85ac-4dc2-9b07-b556bde3e084)

`FLAG:picoCTF{nongshim.shrimp.crackers}`
