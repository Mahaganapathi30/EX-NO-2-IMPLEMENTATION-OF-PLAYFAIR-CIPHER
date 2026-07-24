## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

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



## PROGRAM :
```
#include <stdio.h>
#include <string.h>

char key[5][5] = {
    {'M','O','N','A','R'},
    {'C','H','Y','B','D'},
    {'E','F','G','I','K'},
    {'L','P','Q','S','T'},
    {'U','V','W','X','Z'}
};

void findPos(char ch, int *r, int *c)
{
    if(ch == 'J')
        ch = 'I';

    for(int i = 0; i < 5; i++)
    {
        for(int j = 0; j < 5; j++)
        {
            if(key[i][j] == ch)
            {
                *r = i;
                *c = j;
                return;
            }
        }
    }
}

int main()
{
    char plain[100], text[100];
    int i, j = 0;
    int r1, c1, r2, c2;

    printf("Enter Plain Text: ");
    scanf("%s", plain);

    for(i = 0; plain[i] != '\0'; i++)
    {
        text[j++] = plain[i];

        if(plain[i + 1] == '\0')
        {
            text[j++] = 'X';
            break;
        }

        if(plain[i] == plain[i + 1])
        {
            text[j++] = 'X';
        }
        else
        {
            text[j++] = plain[++i];
        }
    }

    text[j] = '\0';

    printf("Prepared Text : %s\n", text);
    printf("Cipher Text   : ");

    for(i = 0; i < j; i += 2)
    {
        findPos(text[i], &r1, &c1);
        findPos(text[i + 1], &r2, &c2);

        if(r1 == r2)          
        {
            printf("%c%c", key[r1][(c1 + 1) % 5],
                           key[r2][(c2 + 1) % 5]);
        }
        else if(c1 == c2)     
        {
            printf("%c%c", key[(r1 + 1) % 5][c1],
                           key[(r2 + 1) % 5][c2]);
        }
        else                  
        {
            printf("%c%c", key[r1][c2],
                           key[r2][c1]);
        }
    }

    return 0;
}
```
## OUTPUT :

<img width="1365" height="414" alt="image" src="https://github.com/user-attachments/assets/ddef83c3-380c-45c5-8358-e18db05d9b43" />

## RESULT :
Thus the implementation of playfair cipher had been executed successfully.


