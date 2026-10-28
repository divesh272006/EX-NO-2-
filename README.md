## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER
DATE:28-10-2026
 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




Program:
```
#include <stdio.h> 
#include <string.h> 
#include <ctype.h> 
 
char key[5][5]; 
 
void createKey(char word[]) 
{ 
    int used[26] = {0}; 
    int i, j, k = 0; 
    char ch; 
 
    used['j' - 'a'] = 1; 
 
    for (i = 0; word[i] != '\0'; i++) 
    { 
        ch = tolower(word[i]); 
 
        if (ch == 'j') 
            ch = 'i'; 
 
        if (ch >= 'a' && ch <= 'z' && !used[ch - 'a']) 
        { 
            key[k / 5][k % 5] = ch; 
            used[ch - 'a'] = 1; 
            k++; 
        } 
    } 
 
    for (ch = 'a'; ch <= 'z'; ch++) 
    { 
        if (!used[ch - 'a']) 
        { 
            key[k / 5][k % 5] = ch; 
            k++; 
        } 
    } 
} 
 
void findPosition(char ch, int *row, int *col) 
{ 
    int i, j; 
 
    if (ch == 'j') 
        ch = 'i'; 
 
    for (i = 0; i < 5; i++) 
    { 
        for (j = 0; j < 5; j++) 
        { 
            if (key[i][j] == ch) 
            { 
                *row = i; 
                *col = j; 
                return; 
            } 
        } 
    } 
} 
 
int main() 
{ 
    char word[100], text[100], result[200]; 
    int i, n = 0, r1, c1, r2, c2; 
 
    printf("Enter key: "); 
    scanf("%99s", word); 
 
    printf("Enter plain text: "); 
    scanf("%99s", text); 
 
    createKey(word); 
 
    for (i = 0; text[i] != '\0'; i++) 
    { 
        char ch = tolower(text[i]); 
 
        if (ch >= 'a' && ch <= 'z') 
        { 
            if (ch == 'j') 
                ch = 'i'; 
 
            if (n > 0 && result[n - 1] == ch) 
                result[n++] = 'x'; 
 
            result[n++] = ch; 
        } 
    } 
 
    if (n % 2 != 0) 
        result[n++] = 'x'; 
 
    result[n] = '\0'; 
 
    for (i = 0; i < n; i += 2) 
    { 
        findPosition(result[i], &r1, &c1); 
        findPosition(result[i + 1], &r2, &c2); 
 
        if (r1 == r2) 
        { 
            result[i] = key[r1][(c1 + 1) % 5]; 
            result[i + 1] = key[r2][(c2 + 1) % 5]; 
        } 
        else if (c1 == c2) 
        { 
            result[i] = key[(r1 + 1) % 5][c1]; 
            result[i + 1] = key[(r2 + 1) % 5][c2]; 
        } 
        else 
        { 
            result[i] = key[r1][c2]; 
            result[i + 1] = key[r2][c1]; 
        } 
    } 
 
    printf("Cipher text: %s\n", result); 
 
    return 0; 
} 
 
```

Output:

<img width="290" height="201" alt="image" src="https://github.com/user-attachments/assets/2c0395ec-626f-4be9-9825-35af5777a2c6" />

Result:  

The Playfair Cipher program is executed successfully, and the cipher text is cpdwkflz. 

