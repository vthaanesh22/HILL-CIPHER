# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
~~~
import numpy as np

def text_to_numbers(text):
    return [ord(char) - ord('A') for char in text]

def numbers_to_text(numbers):
    return ''.join(chr(num + ord('A')) for num in numbers)

def hill_cipher_encrypt(plaintext, key):
    n = len(key)
    plaintext = plaintext.upper().replace(" ", "")
    while len(plaintext) % n != 0:
        plaintext += 'X'  # Padding with 'X'
    
    text_numbers = text_to_numbers(plaintext)
    key_matrix = np.array(key)
    
    encrypted_numbers = []
    for i in range(0, len(text_numbers), n):
        block = np.array(text_numbers[i:i+n]).reshape(n, 1)
        encrypted_block = np.dot(key_matrix, block) % 26
        encrypted_numbers.extend(encrypted_block.flatten())
    
    return numbers_to_text(encrypted_numbers)

def hill_cipher_decrypt(ciphertext, key):
    n = len(key)
    key_matrix = np.array(key)
    key_inverse = np.linalg.inv(key_matrix) * np.linalg.det(key_matrix)
    key_inverse = np.round(key_inverse).astype(int) % 26  # Modular inverse approximation
    
    text_numbers = text_to_numbers(ciphertext)
    decrypted_numbers = []
    for i in range(0, len(text_numbers), n):
        block = np.array(text_numbers[i:i+n]).reshape(n, 1)
        decrypted_block = np.dot(key_inverse, block) % 26
        decrypted_numbers.extend(decrypted_block.flatten())
    
    return numbers_to_text(decrypted_numbers)

if __name__ == "__main__":
    plaintext = input("Enter plaintext: ")
    key = [[6, 24, 1], [13, 16, 10], [20, 17, 15]]  # Example key matrix
    ciphertext = hill_cipher_encrypt(plaintext, key)
    print("Encrypted Text:", ciphertext)
    decrypted_text = hill_cipher_decrypt(ciphertext, key)
    print("Decrypted Text:", decrypted_text)
~~~

## OUTPUT

![image](https://github.com/user-attachments/assets/c5c8fc52-a9f3-4b47-8f71-a623ba48699d)


## RESULT
Thus, a python program is implement for hill cipher substitution techniques.
