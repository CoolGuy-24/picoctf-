# rotation

In this challenge a file called `encrypted.txt` was provided. The contents of this file were:

>xqkwKBN{z0bib1wv_l3kzgxb3l_25l7k61j}

A hint given was:
> Sometimes rotation is right

Now it was clear that this could be solved by a simple cipher, so since the hint mentioned `rotation` I figured maybe it meant a `ROT` cipher?

So using this [webiste](https://www.cachesleuth.com/rot.html), I was able to test every ROT cipher and on ROT 18 I found the flag.

`FLAG: picoCTF{r0tat1on_d3crypt3d_25d7c61b}`
