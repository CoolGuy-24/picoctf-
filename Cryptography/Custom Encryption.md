#  Custom Encryption

This challenge had two files, the flag_info file which was `enc_flag` and the code file which was `custom_encryption`.

Opening the custom_encryption file helped analyse what type of encryption was done, so that I could reverse the encyrption process and obtain the flag.

The contents of the encryption file were:

```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```

The encryption is a mix of Diffie-Hellman Key Exchange and XOR encryption.

The `generator` function generates the public key value used in Diffie-Hellman Key Exchange. The `encrypt` function mutiplies the ascii value of the character by the kye and by 311. The `is_prime` function checks if the numbers are prime. The `dynamic_xor_encrypt` function reverses the plaintext, XORs the ASCII value with the text key (trudeau) and converts the resukt back into a character and adds it to the encrypted text. The `test` function, integrates all the of the above function to perform the encryption. 


Now to decrypt this encryption, the following code was needed:

```
def generator(g, x, p):
    return pow(g, x) % p

def decrypt(cipher, key):
    decrypted_text = ""
    for number in cipher:
        decrypted_num = number // (key * 311)
        decrypted_text += chr(decrypted_num)
    return decrypted_text

def dynamic_xor_decrypt(ciphertext, text_key):
    decrypted_text = ""
    key_length = len(text_key)
    for i, char in enumerate(ciphertext):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decrypted_text += decrypted_char
    return decrypted_text

a = 97
b = 22
p = 97
g = 31
cipher = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]

u = generator(g, a, p)
v = generator(g, b, p)
shared_key = generator(v, a, p)
ciphertext = decrypt(cipher, shared_key)


original_message = dynamic_xor_decrypt(ciphertext, "trudeau")
original_message = original_message[::-1]

print(original_message)
```

This code performs the Diffie-Hellman Key Exchange to obtain the shared key and decodes the cipher into an intermediate XOR string. Then a XOR decryption is applied using the text key (trudeau) and finally the string is reversed to obtain the original message which is the flag. 

`FLAG: picoCTF{custom_d2cr0pt6d_e4530597}`
