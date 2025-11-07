#include <stdio.h>

int checkRow(int sudoku[9][9], int row) {
    int seen[10] = {0};
    for (int i = 0; i < 9; i++) {
        int num = sudoku[row][i];
        if (num < 1 || num > 9 || seen[num]) return 0;
        seen[num] = 1;
    }
    return 1;
}

int checkCol(int sudoku[9][9], int col) {
    int seen[10] = {0};
    for (int i = 0; i < 9; i++) {
        int num = sudoku[i][col];
        if (num < 1 || num > 9 || seen[num]) return 0;
        seen[num] = 1;
    }
    return 1;
}

int checkBox(int sudoku[9][9], int startRow, int startCol) {
    int seen[10] = {0};
    for (int r = 0; r < 3; r++)
        for (int c = 0; c < 3; c++) {
            int num = sudoku[r + startRow][c + startCol];
            if (num < 1 || num > 9 || seen[num]) return 0;
            seen[num] = 1;
        }
    return 1;
}

int main() {
    int sudoku[9][9];
    printf("Enter 9x9 Sudoku grid:\n");
    for (int i = 0; i < 9; i++)
        for (int j = 0; j < 9; j++)
            scanf("%d", &sudoku[i][j]);

    for (int i = 0; i < 9; i++)
        if (!checkRow(sudoku, i) || !checkCol(sudoku, i)) {
            printf("Invalid Sudoku.\n");
            return 0;
        }

    for (int i = 0; i < 9; i += 3)
        for (int j = 0; j < 9; j += 3)
            if (!checkBox(sudoku, i, j)) {
                printf("Invalid Sudoku.\n");
                return 0;
            }

    printf("Sudoku is valid!\n");
    return 0;
}
