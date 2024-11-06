# Trivial File Transfer Protocol
Reading the forensics page from https://trailofbits.github.io/ctf/forensics/ made me understand `pcap` and `pcapng` files. These are packet capture files which help read the network traffic, by logging them. 
After downloading `Wireshark`, I was able to read the network traffic. 

![image](https://github.com/user-attachments/assets/272d3c59-54df-4cba-b510-79ea13597d0d)

Under the layer of TFTP Protocol, I saw the file `instructions.txt` and then I was wondering how to extract the file. After reasearching on the web, I went to `File --> Export Objects --> TFTP` I saw the object list.

![image](https://github.com/user-attachments/assets/0a6148f6-b772-45be-827c-2588851fbb6a)


I then clicked on `Save All` and then saved those files. I opened the `instructions.txt` and then tried to decode the cipher using different ciphers, and eventually got a readable output using a ROT13 decoder. I got the decoded output as `TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN`
and then I understood to use the `plan.txt` file and decoded again using ROT13 cipher and decoded output to `IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS`

Now I checked the metadata for the three pictures, to find the flag but it lead to nowhere. Reading the webpage again, I tried to carry out stenography analysis on the three pictures using an online tool. After researching more I downloaded the `steghide` command using `sudo install apt steghide` command.
After that I used the command to carry out stenography analysis on the images. It asked for a password so after a while of thinking I got the passphrase to be `DUEDILIGENCE`. Finally, I got the flag from picture3.

```
coolguy24@Vedant-Laptop:~$ cd TFTP
coolguy24@Vedant-Laptop:~/TFTP$ steghide extract -sf ./picture1.bmp
Enter passphrase:
steghide: could not extract any data with that passphrase!
coolguy24@Vedant-Laptop:~/TFTP$ steghide extract -sf ./picture2.bmp
Enter passphrase:
steghide: could not extract any data with that passphrase!
coolguy24@Vedant-Laptop:~/TFTP$ steghide extract -sf ./picture3.bmp
Enter passphrase:
wrote extracted data to "flag.txt".
```


FLAG: `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`
