# EXPT.NO.09-IMPLEMENTATION-OF-ERROR-DETECTION-USING-CRC-CCITT-16-BIT-TECHNIQUE
# AIM:
To write a program for error Detection using Cyclic Redundancy Check (CRC-16 bit) technique.

# EQUIPMENTS REQUIRED:
1.	Personal Computer
2.	C++ compiler

# ALGORITHM:
  1. Open code blocks application and create a new file.
  2. After creating the file type the codes.
  3. After typing the codes save the file using the .c extension in the desired location.
  4. Run the program using build and run.
  5. Give polynomial values and the generated polynomial is obtained, and by other means arraive	at the desired output which uses the error detection technique.
  6. Thus the output polynomial is obtained through this technique.

# PROGRAM:
```
#include <stdio.h>
#include <string.h>
#define N 3   // Length of generator polynomial
char t[128], cs[128], g[] = "111";
int a, e, c;
void xor_op() {
    for (c = 1; c < N; c++)
        cs[c] = ((cs[c] == g[c]) ? '0' : '1');
}
void crc() {
    for (e = 0; e < N; e++)
        cs[e] = t[e];
    do {
        if (cs[0] == '1')
            xor_op();
        for (c = 0; c < N - 1; c++)
            cs[c] = cs[c + 1];
        cs[c] = t[e++];
    } while (e <= a + N - 1);
}
int main() {
    printf("\nEnter poly: ");
    scanf("%s", t);
    printf("\nGen poly is: %s", g);
    a = strlen(t);
    // Append N-1 zeros
    for (e = a; e < a + N - 1; e++)
        t[e] = '0';
    t[e] = '\0';
    printf("\nModified t[u]: %s", t);
    crc();
    printf("\nChecksum is: %s", cs);
    // Append checksum to message
    for (e = a; e < a + N - 1; e++)
        t[e] = cs[e - a];
    t[e] = '\0';
    printf("\nFinal code word is: %s", t);
    printf("\nTest error detection 0(yes) 1(no)?: ");
    scanf("%d", &e);
    if (e == 0) {
        int pos;
        printf("Enter position where error is to be inserted: ");
        scanf("%d", &pos);
        t[pos] = (t[pos] == '0') ? '1' : '0';
        printf("Erroneous data: %s\n", t);
    }
    crc();
    for (e = 0; (e < N - 1) && (cs[e] != '1'); e++);
    if (e < N - 1)
        printf("Error detected\n");
    else
        printf("No error detected\n");
    return 0;
}
``` 
# OUTPUT:
<img width="1461" height="273" alt="image" src="https://github.com/user-attachments/assets/da77b689-5436-4a43-b962-d426e66c7814" />

# RESULT:
Thus the error detection using CRC-CCITT[16 bit] technique is implemented and the output is obtained and verified successfully.
