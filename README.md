# Lab-Exercise---2---Playfair-Cipher
## Aim 
To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.
## Procedure
```
Step 1: Design of PlayFair Cipher algorithm
Step 2: Implementation using C or python code
Step 3: Testing algorithm with different key values.
```
## Program
```
def generate_matrix(key):
    key = key.upper().replace("J", "I")
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    text = ""
    
    for ch in key + alphabet:
        if ch.isalpha() and ch not in text:
            text += ch
            
    return [list(text[i:i+5]) for i in range(0, 25, 5)]

def prepare_text(text):
    text = text.upper().replace("J", "I")
    text = "".join([ch for ch in text if ch.isalpha()])
    pairs = []
    i = 0
    
    while i < len(text):
        a = text[i]
        
        if i + 1 == len(text):
            b = 'X'
            i += 1
        elif text[i] == text[i + 1]:
            b = 'X'
            i += 1
        else:
            b = text[i + 1]
            i += 2
            
        pairs.append(a + b)
        
    return pairs

def playfair_encrypt(plaintext, key):
    matrix = generate_matrix(key)
    pairs = prepare_text(plaintext)
    ciphertext = ""
    
    def position(ch):
        for r in range(5):
            for c in range(5):
                if matrix[r][c] == ch:
                    return r, c
                    
    for pair in pairs:
        r1, c1 = position(pair[0])
        r2, c2 = position(pair[1])
        
        if r1 == r2: # Same row
            ciphertext += matrix[r1][(c1 + 1) % 5]
            ciphertext += matrix[r2][(c2 + 1) % 5]
        elif c1 == c2: # Same column
            ciphertext += matrix[(r1 + 1) % 5][c1]
            ciphertext += matrix[(r2 + 1) % 5][c2]
        else: # Rectangle rule
            ciphertext += matrix[r1][c2]
            ciphertext += matrix[r2][c1]
            
    return matrix, pairs, ciphertext

key = input("Enter the key: ")
plaintext = input("Enter the plaintext: ")

matrix, pairs, encrypted = playfair_encrypt(plaintext, key)

print("\nKey Matrix:")
for row in matrix:
    print(" ".join(row))
    
print("\nPlaintext pairs:", ", ".join(pairs))
print("Encrypted text:", encrypted)
```
## Output
<img width="1917" height="990" alt="image" src="https://github.com/user-attachments/assets/d0c11ffa-2840-4dcf-b34c-ebd93abff87e" />


## Result
The program is executed successfully. 
