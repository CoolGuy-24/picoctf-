# miniRSA

In this challenge a file called `ciphertext` is provided which has the following contents:

```
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872650073010782049179856976080512716237308882294226369300412719995904064931819531456392957957122459640736424089744772221933500860936331459280832211445548332429338572369823704784625368933 
```

The challenge also had 3 hints:

1st Hint:
`RSA` [tutorial](https://en.wikipedia.org/wiki/RSA_(cryptosystem))

2nd Hint:
`How could having too small an e affect the security of this 2048 bit key?`

3rd Hint:
`Make sure you don't lose precision, the numbers are pretty big (besides the e value)`

I read up on RSA and tried to understand it as much as I could. here is what I have undertsood from it.

 RSA is an asymettric encryption so a public key is known to all where as the private key is known only to the person decrypting the message.
 
*  A message `M` is converted to an integer `m`. This can be done by converting the message into its ASCII Value.
  
* The public key is (n, e) and the private key is (n, d).
>  `n` = `p` x `q`
> where p and q are very large prime numbers

* `n` should be larger than `m`
* Next, we need to choose an integer e such that
  > 1 < e < ϕ(n) and gcd(e, ϕ(n)) = 1, where ϕ(n) = (p-1)*(q-1) is Euler’s totient function. This value of e will be the public key exponent.
  
* `d` is calculated using the formula
  > d × e ≡ 1(modϕ(n))
 
* A ciphertext `c` is obtained by using the formula
> c = m<sup>e</sup> (mod n)

* Now the private and public key are available

* Decrypt the message using the formula
  >m = c<sup>d</sup> (mod n)
  

  After having understood how RSA works I looked at the challenge file again.

  I had the public key, (`n`,`e`) and the ciphertext `c`. Factoring `n` to obtain `p` and `q` would be extremely difficult and would require lots of computing power. So I needed to find another way to get the value of `p` and `q` so that I could get the value of `d` and decrypt the message.

  I looked over at the hints and realised maybe it has got to do something with a low value of `e` and searching up I got to know about a small exponent attack that can be used on RSA.

  [This](https://crypto.stackexchange.com/questions/6713/low-public-exponent-attack-for-rsa) says that for a small public exponent like `e = 3` the valueof m is simply the cube root of `c`. So now all I need to do was find a way to compute the cube of  avery large number. I found a python code to do the same.

```
def find_invpow(x,n):
    """Finds the integer component of the n'th root of x,
    an integer such that y ** n <= x < (y + 1) ** n.
    """
    high = 1
    while high ** n < x:
        high *= 2
    low = high/2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1
  ```

Using this code, I found m to be:
`m = 13016382529449106065894479374027604750406953699090365388203708028670029596145277`

Now I tried to convert this into text and then I got the flag as:

`FLAG:{}`
