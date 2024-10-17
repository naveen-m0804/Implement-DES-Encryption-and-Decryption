# DES Encryption and Decryption

## Aim

To implement DES encryption and decryption using any programming language to secure a given plaintext message.


## Procedure

1. **Understand the DES Algorithm**  
   DES is a symmetric encryption algorithm that uses a 56-bit key. It operates on 64-bit data blocks and encrypts the plaintext through 16 rounds of permutation and substitution.

2. **Set Up the Development Environment**  
   Install the necessary cryptographic library. For Python, install `pycryptodome` using the following command:  
   ```bash
   pip install pycryptodome
   ```

3. **Design the Program**  
   Implement functions to handle both encryption and decryption processes. Make sure to take the key and message as inputs.

4. **Encrypt the Plaintext**  
   Write a function that uses the DES algorithm to convert the given plaintext into ciphertext. If using Python, you can use the ECB (Electronic Codebook) mode from the `DES` class in the `Crypto.Cipher` module.

5. **Decrypt the Ciphertext**  
   Write a function that decrypts the ciphertext using the same key. Ensure that after decryption, the original message matches the input plaintext.

6. **Test the Program**  
   Test the encryption and decryption functions using various plaintext messages and keys. Verify the outputs.

7. **Record the Results**  
   Show the output for both encryption and decryption steps.

## Program (Python Example)

### Encryption
```python
import base32hex
import hashlib
from Crypto.Cipher import DES
password = "Password"
salt = '\x28\xAB\xBC\xCD\xDE\xEF\x00\x33'
key = password + salt
m = hashlib.md5(key)
key = m.digest()
(dk, iv) =(key[:8], key[8:])
crypter = DES.new(dk, DES.MODE_CBC, iv)

plain_text= "I see you"

print("The plain text is : ",plain_text)
plain_text += '\x00' * (8 - len(plain_text) % 8)
ciphertext = crypter.encrypt(plain_text)
encode_string= base32hex.b32encode(ciphertext)
print("The encoded string is : ",encode_string)
```


### Decryption 

```python
import base32hex
import hashlib
from Crypto.Cipher import DES
password = "Password"
salt = '\x28\xAB\xBC\xCD\xDE\xEF\x00\x33'
key = password + salt
m = hashlib.md5(key)
key = m.digest()
(dk, iv) =(key[:8], key[8:])
crypter = DES.new(dk, DES.MODE_CBC, iv)

encrypted_string='UH562EGM8RCHHTOUC5CTRS59OG======'

print("The ecrypted string is : ",encrypted_string)
encrypted_string=base32hex.b32decode(encrypted_string)
decrypted_string = crypter.decrypt(encrypted_string)
print("The decrypted string is : ",decrypted_string)
```
## Output

![image](https://github.com/user-attachments/assets/b68266e0-bab9-40ff-82d0-a8ceefa052e2)
![image](https://github.com/user-attachments/assets/1a6aa812-6ddc-42ff-a639-96f0b7560085)


## Result

The DES encryption and decryption were successfully implemented. The ciphertext was generated from the given plaintext, and the original message was retrieved upon decryption, verifying that the DES algorithm works correctly. However, due to the small key size, DES is considered insecure for modern applications.
