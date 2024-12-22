# SRA

In this challenge there was a NetCat link provided and the code for the program in the file `chal.py`. There were no hints given for this challenge but it was pretty much clear that it is somethign related to RSA.

I conected to the link and ran the program. I tested it with `hello` to see what is the output.

```
coolguy24@Vedant-Laptop:~$ nc saturn.picoctf.net 61981
anger = 7688327224125727654746276361068774089709319145698473827758983686727556395258
envy = 17639316489639822565965437498492670675341869017347981871576442541396456561929
vainglory?
> hello
hello
Hubris!
```
I looked at the `chal.py` file.

```
from Crypto.Util.number import getPrime, inverse, bytes_to_long
from string import ascii_letters, digits
from random import choice

pride = "".join(choice(ascii_letters + digits) for _ in range(16))
gluttony = getPrime(128)
greed = getPrime(128)
lust = gluttony * greed
sloth = 65537
envy = inverse(sloth, (gluttony - 1) * (greed - 1))

anger = pow(bytes_to_long(pride.encode()), sloth, lust)

print(f"{anger = }")
print(f"{envy = }")

print("vainglory?")
vainglory = input("> ").strip()

if vainglory == pride:
    print("Conquered!")
    with open("/challenge/flag.txt") as f:
        print(f.read())
else:
    print("Hubris!")

```

It was pretty clear that there was RSA encryption used in this, with `lust`,`gluttony` and `greed` corresponding to the `n`, `p` and `q` values in a normal RSA encryption.
`sloth` is the public key exponent, `e`.

It was also clear that the flag would be revealed once the prompt has the value of the `pride` variable. To find the `pride` variable value I would need the value of `anger`,`envy` and `lust`.

The value of `anger` and `envy` is provided but not `lust`. I thought of 
