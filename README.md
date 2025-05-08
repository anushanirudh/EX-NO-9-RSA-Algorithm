# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
# Name : R ANIRUDH
# Reg No : 212223230016

```
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def mod_exp(base, exp, mod):
    result = 1
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        base = (base * base) % mod
        exp = exp // 2
    return result

def mod_inverse(e, phi):
    t, newt = 0, 1
    r, newr = phi, e
    while newr != 0:
        quotient = r // newr
        t, newt = newt, t - quotient * newt
        r, newr = newr, r - quotient * newr
    if r > 1:
        return -1  # No modular inverse
    if t < 0:
        t += phi
    return t

def main():
    # Step 1: Choose primes
    p = 61
    q = 53

    # Step 2: Compute n and phi
    n = p * q
    phi = (p - 1) * (q - 1)

    # Step 3: Choose e
    e = 17
    if gcd(e, phi) != 1:
        print("e and phi(n) are not coprime!")
        return

    # Step 4: Calculate d
    d = mod_inverse(e, phi)
    if d == -1:
        print("No modular inverse found for e!")
        return

    # Step 5: Display keys
    print(f"Public Key: (e = {e}, n = {n})")
    print(f"Private Key: (d = {d}, n = {n})")

    # Step 6: Get message
    message = input("Enter a message to encrypt (alphabetic characters only): ")

    # Step 7: Encrypt
    encrypted = [mod_exp(ord(char), e, n) for char in message]
    print("\nEncrypted Message:")
    print(' '.join(str(num) for num in encrypted))

    # Step 8: Decrypt
    decrypted = ''.join(chr(mod_exp(char, d, n)) for char in encrypted)
    print("\nDecrypted Message:")
    print(decrypted)

if __name__ == "__main__":
    main()
```




## Output:

![image](https://github.com/user-attachments/assets/da578bd4-08a8-4aa4-9108-af1adf76c48a)




## Result:
 The program is executed successfully.
