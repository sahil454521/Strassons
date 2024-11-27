# Strassons
#include <stdio.h>
#include <stdlib.h>


#define THRESHOLD 2


void add(int n, int a[n][n], int b[n][n], int result[n][n]) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            result[i][j] = a[i][j] + b[i][j];
        }
    }



void subtract(int n, int a[n][n], int b[n][n], int result[n][n]) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            result[i][j] = a[i][j] - b[i][j];
        }
    }



void regularMultiply(int n, int a[n][n], int b[n][n], int result[n][n]) {
    for (int i = 0; i < n; i+) {
        for (int j = 0; j < n; j++) {
            result[i][j] = 0;
            for (int k = 0; k < n; k++) {
                result[i][j] = a[i][k] * b[k][j];
            }
        }
    }
}


void strassen(int n, int a[n][n], int b[n][n], int c[n][n]) {
    if (n <= THRESHOLD) {
        regularMultiply(n, a, b, c);
        return;
    }

  int newSize = n / 2;

   
  int (*a00)[newSize] = malloc(newSize * newSize * sizeof(int));
  int (*a01)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*a10)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*a11)[newSize] = malloc(newSize * newSize * sizeof(int));
        
  int (*b00)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*b01)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*b10)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*b11)[newSize] = malloc(newSize * newSize * sizeof(int));
        int (*m1)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m2)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m3)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m4)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m5)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m6)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*m7)[newSize] = malloc(newSize * newSize * sizeof(int));
        int (*temp1)[newSize] = malloc(newSize * newSize * sizeof(int));
            int (*temp2)[newSize] = malloc(newSize * newSize * sizeof(int));
        for (int i = 0; i < newSize; i++) {
                for (int j = 0; j < newSize; j++) {
                    a00[i][j] = a[i][j];
                    a01[i][j] = a[i][j + newSize];
                    a10[i][j] = a[i + newSize][j];
                    a11[i][j] = a[i + newSize][j + newSize];
                    b00[i][j] = b[i][j];
                    b01[i][j] = b[i][j + newSize];
                    b10[i][j] = b[i + newSize][j];
                    b11[i][j] = b[i + newSize][j + newSize];
                }
            }
        
         
add(newSize, a00, a11, temp1);
            add(newSize, b00, b11, temp2);
            strassen(newSize, temp1, temp2, m1); 
  add(newSize, a10, a11, temp1);
            strassen(newSize, temp1, b00, m2);   
subtract(newSize, b01, b11, temp2);
            strassen(newSize, a00, temp2, m3);   
  subtract(newSize, b10, b00, temp2);
            strassen(newSize, a11, temp2, m4)  
        
  add(newSize, a00, a01, temp1);
            strassen(newSize, temp1, b11, m5);
        
            
  subtract(newSize, a10, a00, temp1);
            add(newSize, b00, b01, temp2);
            strassen(newSize, temp1, temp2, m6);
  subtract(newSize, a01, a11, temp1);
            add(newSize, b10, b11, temp2);
            strassen(newSize, temp1, temp2, m7);
  add(newSize, m1, m4, temp1);
            subtract(newSize, temp1, m5, temp2);
            add(newSize, temp2, m7, c);
        free(a00); free(a01); free(a10); free(a11);
            free(b00); free(b01); free(b10); free(b11);
            free(m1); free(m2); free(m3); free(m4);
            free(m5); free(m6); free(m7);
            free(temp1); free(temp2);
}

int main() {
    int n;

  printf("Enter the size of the matrices: ");
    scanf("%d", &n);

  int a[n][n], b[n][n], c[n][n];

   printf("Enter elements of the first matrix:");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &a[i][j]);
        }
    }

  printf("Enter elements of the second matrix:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &b[i][j]);
        }
    }

  strassen(n, a, b, c);

  printf("Resultant matrix:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", c[i][j]);
        }
        printf("\n");
    }

  return 0;
}


}
