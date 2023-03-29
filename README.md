#include <stdio.h>
#include <string.h>

struct sinhvien {
    char HT[50];  // s? d?ng m?ng k? t? đ? lưu h? tên
    int MSSV;
    float DiemTK;
    float DiemGK;
    float DiemCK;
    float DiemTH;
    float DiemTB;
};

void Input(sinhvien A[], int &n) {
    printf("Nhap so luong sinh vien ban can quan li: ");
    scanf("%d", &n);
    getchar();  
    for (int i = 0; i < n; i++) {
        printf("\nNhap Ho Ten Sinh Vien thu %d: ", i+1);
        gets(A[i].HT);
        printf("Nhap MSSV: ");
        scanf("%d", &A[i].MSSV);
        printf("Nhap Diem Thuong Ki: ");
        scanf("%f", &A[i].DiemTK);
        printf("Nhap Diem Giua Ki: ");
        scanf("%f", &A[i].DiemGK);
        printf("Nhap Diem Cuoi Ki: ");
        scanf("%f", &A[i].DiemCK);
        printf("Nhap Diem Thuc Hanh: ");
        scanf("%f", &A[i].DiemTH);
        getchar(); 
    }
}

void Output(sinhvien A[], int n) {
    printf("+------+----------------------+----------------------+------------+\n");
    printf("| STT  | Ho Ten               | MA SINH VIEN         |    Diem TB |\n");
    printf("+------+----------------------+----------------------+------------+\n");
    for (int i = 0; i < n; i++) {
        A[i].DiemTB = (((2 * A[i].DiemTK + 3 * A[i].DiemGK + 5 * A[i].DiemCK) / 10) * 2 + A[i].DiemTH) / 3;
        printf("| %4d | %s | %-20d | %10.2f |\n", i+1, A[i].HT, A[i].MSSV, A[i].DiemTB);
    }
    printf("+------+----------------------+----------------------+------------+\n");
}
void Outputhoclai(sinhvien A[], int n) {
    printf("+------+----------------------+----------------------+------------+\n");
    printf("| STT  | Ho Ten               | MA SINH VIEN         |    Diem TB |\n");
    printf("+------+----------------------+----------------------+------------+\n");
    for (int i = 0; i < n; i++) {
        A[i].DiemTB = (((2 * A[i].DiemTK + 3 * A[i].DiemGK + 5 * A[i].DiemCK) / 10) * 2 + A[i].DiemTH) / 3;
        if(A[i].DiemTB<4) 
		printf("| %4d | %s | %-20d | %10.2f |\n", i+1, A[i].HT, A[i].MSSV, A[i].DiemTB);
    }
    printf("+------+----------------------+----------------------+------------+\n");
}
void TimSV(sinhvien A[], int n, int &mssv) {
	printf("Nhap MSSV ban can tim: ");
	scanf("%d", &mssv);
	int STT=1;
	for(int i=1; i<n ; i++) {
		if(A[i].MSSV==mssv) {
			printf("+------+----------------------+----------------------+------------+\n");
    		printf("| STT  | Ho Ten               | MA SINH VIEN         |    Diem TB |\n");
    		printf("+------+----------------------+----------------------+------------+\n");
    		printf("| %4d | %s | %-20d | %10.2f |\n", STT++, A[i].HT, A[i].MSSV, A[i].DiemTB);
    }
		}
	if(STT==1) printf("Khong tim thay\n");
	}
void SapXep(sinhvien A[], int n) {
	void DSDiem(sinhvien A[], int n);
	for(int i=0;  i<n;i++) {
		for(int j=i+1;j<n;j++) {
			if(  A[i].DiemTB < A[j].DiemTB ) {
				sinhvien temp = A[i];
				A[i] = A[j];
				A[j] = temp;
			}
		}
	}
	DSDiem(A, n); 
	printf("-------------------\n");
}
void DSDiem(sinhvien A[], int n) {
	printf("+------+----------------------+----------------------+----------+----------+----------+----------+-----------+---------------+\n");
    printf("| STT  | Ho Ten               | MA SINH VIEN         |    TK    |    GK    |    CK    |    TH    |  Diem TB  |    GHI CHU    |\n");
    printf("+------+----------------------+----------------------+----------+----------+----------+----------+-----------+---------------+\n");
    for (int i = 0; i < n; i++) {
        A[i].DiemTB = (((2 * A[i].DiemTK + 3 * A[i].DiemGK + 5 * A[i].DiemCK) / 10) * 2 + A[i].DiemTH) / 3;
        printf("| %4d | %s | %-20d | %10.2f | %10.2f | %10.2f | %10.2f | %10.2f |", i+1, A[i].HT, A[i].MSSV, A[i].DiemTK, A[i].DiemGK, A[i].DiemCK, A[i].DiemTH, A[i].DiemTB);
        if(A[i].DiemTB<4) printf(" Hoc lai |\n");
        else if(A[i].DiemTB>=4) printf("         |\n");
    }
     printf("+------+----------------------+----------------------+----------+----------+----------+----------+-----------+---------------+\n");
}

int main() {
    sinhvien A[100];
    int n,mssv;
    Input(A, n);
    Output(A, n);
    Outputhoclai(A, n);
	TimSV(A, n, mssv);

	SapXep(A , n);
	DSDiem(A, n);
    return 0;
}
