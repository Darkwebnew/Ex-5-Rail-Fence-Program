# Ex-5 RAIL FENCE

<br>

## DATE:

<br>

## AIM:

<br>

To develop a simple C program to implement Rail Fence Cipher.

<br>

## DESIGN STEPS:

<br>

Step 1: Design of Rail Fence Cipher algorithnm

<br>

Step 2: Implementation using C or pyhton code

<br>

Step 3: Testing algorithm with different key values.

<br>

## PROGRAM:

<br>

```
#include <iostream>
#include <cstring>
using namespace std;

// Function to perform Rail Fence Cipher encryption
string railFenceEncrypt(string text, int rails) {
    if (rails == 1) return text;

    string result = "";
    int len = text.length();
    char rail[rails][len];
    
    // Initialize the rail matrix with NULL characters
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    bool down = false;  // Direction flag (down or up the rails)
    int row = 0, col = 0;

    // Fill the rail matrix
    for (int i = 0; i < len; i++) {
        if (row == 0 || row == rails - 1) down = !down;  // Change direction at top or bottom rail

        rail[row][col++] = text[i];  // Place character in the matrix

        row += down ? 1 : -1;  // Move to the next rail
    }

    // Read the matrix row-wise to get the encrypted text
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                result += rail[i][j];

    return result;
}

// Function to perform Rail Fence Cipher decryption
string railFenceDecrypt(string cipher, int rails) {
    if (rails == 1) return cipher;

    int len = cipher.length();
    char rail[rails][len];
    
    // Initialize the rail matrix with NULL characters
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    // Mark the positions in the matrix where characters will go
    bool down = false;
    int row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        if (row == 0 || row == rails - 1) down = !down;

        rail[row][col++] = '*';  // Mark position

        row += down ? 1 : -1;
    }

    // Fill the rail matrix with the ciphertext
    int index = 0;
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    // Read the matrix zig-zag to get the decrypted text
    string result = "";
    row = 0, col = 0;
    down = false;

    for (int i = 0; i < len; i++) {
        if (row == 0 || row == rails - 1) down = !down;

        result += rail[row][col++];

        row += down ? 1 : -1;
    }

    return result;
}

int main() {
    string message;
    int rails;

    cout << "Enter a Secret Message: ";
    getline(cin, message);

    cout << "Enter number of rails: ";
    cin >> rails;

    // Encrypt the message
    string encryptedMessage = railFenceEncrypt(message, rails);
    cout << "Encrypted Message: " << encryptedMessage << endl;

    // Decrypt the message
    string decryptedMessage = railFenceDecrypt(encryptedMessage, rails);
    cout << "Decrypted Message: " << decryptedMessage << endl;

    return 0;
}
```

<br>

## OUTPUT:

<br>

![image](https://github.com/user-attachments/assets/28a62870-7554-4ffa-9771-042934b1df7e)

<br>

## RESULT:

<br>

The program is executed successfully
