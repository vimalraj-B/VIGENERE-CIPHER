# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM
## Developed By : VIMALRAJ B
## Register Number : 212224230304

```

#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to generate the repeated key
void generateKey(char* plaintext, char* key, char* newKey) {
    int ptLen = strlen(plaintext);
    int keyLen = strlen(key);
    int j = 0;

    for (int i = 0; i < ptLen; i++) {
        if (isalpha(plaintext[i])) { // Only letters
            newKey[i] = key[j % keyLen];
            j++;
        } else {
            newKey[i] = plaintext[i]; // Keep non-letter characters as is
        }
    }
    newKey[ptLen] = '\0';
}

// Encryption function
void encrypt(char* plaintext, char* key, char* ciphertext) {
    int len = strlen(plaintext);
    for (int i = 0; i < len; i++) {
        if (isupper(plaintext[i])) {
            ciphertext[i] = ((plaintext[i] - 'A') + (toupper(key[i]) - 'A')) % 26 + 'A';
        } else if (islower(plaintext[i])) {
            ciphertext[i] = ((plaintext[i] - 'a') + (tolower(key[i]) - 'a')) % 26 + 'a';
        } else {
            ciphertext[i] = plaintext[i]; // Non-letter characters
        }
    }
    ciphertext[len] = '\0';
}

// Decryption function
void decrypt(char* ciphertext, char* key, char* plaintext) {
    int len = strlen(ciphertext);
    for (int i = 0; i < len; i++) {
        if (isupper(ciphertext[i])) {
            plaintext[i] = ((ciphertext[i] - 'A') - (toupper(key[i]) - 'A') + 26) % 26 + 'A';
        } else if (islower(ciphertext[i])) {
            plaintext[i] = ((ciphertext[i] - 'a') - (tolower(key[i]) - 'a') + 26) % 26 + 'a';
        } else {
            plaintext[i] = ciphertext[i]; // Non-letter characters
        }
    }
    plaintext[len] = '\0';
}

int main() {
    char plaintext[1000], key[100], newKey[1000], ciphertext[1000], decryptedText[1000];

    printf("Enter plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = 0; // Remove newline

    printf("Enter key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = 0; // Remove newline

    generateKey(plaintext, key, newKey);

    encrypt(plaintext, newKey, ciphertext);
    printf("Encrypted text: %s\n", ciphertext);

    decrypt(ciphertext, newKey, decryptedText);
    printf("Decrypted text: %s\n", decryptedText);

    return 0;
}
```
## OUTPUT
<img width="452" height="271" alt="image" src="https://github.com/user-attachments/assets/fd5baf01-071f-49e0-a6ba-59ecefebe3b5" />

## RESULT

Thus the program executed successfully
