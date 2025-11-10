## EX : 3 IMPLEMENTATION OF HILL CIPHER

## AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

Step 1:

Design of Hill Cipher algorithnm

Step 2:

Implementation using C or pyhton code

Step 3:

1.	Convert each letter of the message to a number (A = 0, B = 1, ..., Z = 25) and divide the message into blocks of size n.
2.	Select an invertible n × n matrix as the cipher key (modulo 26 for the English alphabet).
3.	Multiply each block of n letters by the cipher key matrix (modulo 26) to get the encrypted numbers.
4.	Convert the encrypted numbers back into letters using the reverse of step 1.
5.	Multiply the encrypted blocks by the inverse of the cipher key matrix (modulo 26) to recover the original message.
6.	Ensure the key matrix is invertible (mod 26) for decryption to be possible.


## PROGRAM:

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 2   // Using 2x2 key matrix

// Function to multiply key matrix with plaintext vector
void encrypt(int key[SIZE][SIZE], int pt[SIZE], int ct[SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        ct[i] = 0;
        for (int j = 0; j < SIZE; j++) {
            ct[i] += key[i][j] * pt[j];
        }
        ct[i] %= 26;
    }
}

int main() {
    char plaintext[100] = "MAHA SHREE";   // Hardcoded input
    char ciphertext[100];
    int key[SIZE][SIZE];
    int pt[SIZE], ct[SIZE];
    int n, k = 0;

    // Key matrix (example, invertible mod 26)
    key[0][0] = 3; key[0][1] = 3;
    key[1][0] = 2; key[1][1] = 5;

    // Preprocess plaintext: remove spaces, convert to uppercase
    n = strlen(plaintext);
    for (int i = 0; i < n; i++) {
        if (isalpha(plaintext[i])) {
            plaintext[k++] = toupper(plaintext[i]);
        }
    }
    plaintext[k] = '\0';

    // If odd length, pad with X
    if (k % 2 != 0) {
        plaintext[k++] = 'X';
        plaintext[k] = '\0';
    }

    printf("Plaintext (processed): %s\n", plaintext);

    // Encrypt in pairs
    int cpos = 0;
    for (int i = 0; i < k; i += SIZE) {
        for (int j = 0; j < SIZE; j++)
            pt[j] = plaintext[i + j] - 'A';  // convert letter to number (0–25)

        encrypt(key, pt, ct);

        for (int j = 0; j < SIZE; j++)
            ciphertext[cpos++] = ct[j] + 'A';  // back to letters
    }
    ciphertext[cpos] = '\0';

    printf("Ciphertext: %s\n", ciphertext);

    return 0;
}
```
## OUTPUT:

<img width="789" height="343" alt="Screenshot 2025-09-22 143747" src="https://github.com/user-attachments/assets/571d3062-6dc7-4a52-b250-9230b498db8c" />

## RESULT:
