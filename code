#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    FILE *train;

    train = fopen(argv[1], "r");

    char first[40];

    int row = 0;

    int column = 0;

    fscanf(train, "%s", first);

    fscanf(train, "%d", &column);

    fscanf(train, "%d", &row);

    column = column+1;

    double **x = (double **)malloc((row) * sizeof(double *));

    for (int i = 0; i < row; i++) {
        x[i] = (double*)malloc((column) * sizeof(double));
    }
    double *y = (double *)malloc((row) * sizeof(double *));

    for (int i = 0; i < row;i++) {

        x[i][0] = 1;

    }
    for (int i = 0; i < row; i++) {

        for (int j = 1; j < column; j++) {

            fscanf(train, "%lf", &x[i][j]);

        }

        fscanf(train, "%lf", &y[i]);
    }

    double **temp = (double **)malloc((column) * sizeof(double*));


    double **temp2 = (double **)malloc((column) * sizeof(double *));

    for (int i = 0; i < column; i++) {

        temp[i] = (double*)malloc((column) * sizeof(double));

    }

    for (int i = 0; i < column; i++) {

        temp2[i] = (double*)malloc((column) * sizeof(double));

    }

    for (int i = 0; i < column; i++) {

        for(int j =0; j< column; j++) {

            temp2[i][j] = 0;

        }

    }

    for (int k = 0; k < row; k++) {

        for (int i = 0; i < column; i++) {

            for (int j = 0; j < column; j++) {

                temp[i][j] = x[k][j] * x[k][i];

                temp2[i][j] += temp[i][j];

            }

        }

    }

    double **inv = (double **)malloc((column) * sizeof(double*));

    for (int i = 0; i < column; i++) {

        inv[i] = (double*)malloc((column) * sizeof(double));

    }

    for(int i = 0; i < column; i++) {

        for(int j = 0; j < column; j++) {

            if (i == j) {

                inv[i][j] = 1;

            }

            else {

                inv[i][j] = 0;

            }

        }

    }

    for(int i = 0; i < column; i++) {

        if (temp2[i][i] != 1) {

            double multiple = temp2[i][i];

             for(int j = 0; j < column; j++) {
                 temp2[i][j] = (temp2[i][j])/multiple;

                 inv[i][j] = (inv[i][j])/multiple;

             }

        } 

        for(int k = 0; k < column; k++) {

            if(k != i) {

                double f = -temp2[k][i];

                for(int j = 0; j < column; j++) {

                    temp2[k][j] = (f* temp2[i][j])+temp2[k][j];

                    inv[k][j] = (f * inv[i][j])+inv[k][j];

                }

            }

        }

    }

    double **temp3 = (double **)malloc((column) * sizeof(double *));

    double **temp4 = (double **)malloc((column) * sizeof(double *));

    for (int i = 0; i < column; i++) {

        temp3[i] = (double*)malloc((row) * sizeof(double));

    }

    for (int i = 0; i < column; i++) {

        temp4[i] = (double*)malloc((row) * sizeof(double));
    }

     for (int i = 0; i < column; i++) {

        for(int j =0; j< row; j++) {

            temp4[i][j] = 0;

        }

    }

    for (int k = 0; k < column; k++) {

        for (int i = 0; i < column; i++) {

            for (int j = 0; j < row; j++) {

                temp3[i][j] = inv[i][k] * x[j][k];

                temp4[i][j] += temp3[i][j];

            }

        }

    }

    double *w = (double *)malloc((column) * sizeof(double *));

    double *temp5 = (double *)malloc((column) * sizeof(double *));

    for(int i =0; i <column;i++) {

        w[i] = 0;

    }

    for(int i = 0; i < row; i++) {

        for(int j = 0; j<column;j++) {

            temp5[j] = y[i]*temp4[j][i];

            w[j] += temp5[j];

        }

    }

    FILE *data;

    data = fopen(argv[2], "r");

    char secondWord[40];

    fscanf(data, "%s", secondWord);

    int col2;

    int row2;

    fscanf(data, "%d", &col2);

    fscanf(data, "%d", &row2);

    double **dat = (double **)malloc((row2) * sizeof(double *));

    for (int i = 0; i < row2; i++) {

        dat[i] = (double*)malloc((col2+1) * sizeof(double));

    }
    for (int i = 0; i < row2;i++) {

        dat[i][0] = 1.0;

    }
    for (int i = 0; i < row2; i++) {

        for (int j = 1; j < col2+1; j++) {

            fscanf(data, "%lf", &dat[i][j]);

        }
    }

    double *temp6 = (double *)malloc((row2) * sizeof(double *));

    double *ans = (double *)malloc((row2) * sizeof(double *));

    for(int i =0; i <row2;i++) {

        ans[i] = 0;

    }

    for(int i = 0; i < column; i++) {

        for(int j = 0; j < row2; j++) {

            temp6[j] = dat[j][i]*w[i];

            ans[j] += temp6[j];

        }

    }
    for(int i = 0; i <row2; i++) {

        printf("%.0f\n", ans[i]);

    }

    for (int i = 0; i < row; i++) {

        free(x[i]);

    }

    for (int i = 0; i < row2; i++) {
        free(dat[i]);
    }

    for (int i = 0; i < column; i++) {

        free(inv[i]);

        free(temp[i]);

        free(temp2[i]);
        
        free(temp3[i]);

        free(temp4[i]);
    }
    free(ans);
    free(dat);
    free(inv);
    free(temp);
    free(temp2);
    free(temp3);
    free(temp4);
    free(temp5);
    free(temp6);
    free(w);
    free(x);
    free(y);
}
