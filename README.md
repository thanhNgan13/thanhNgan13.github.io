# thanhNgan13.github.io
#include <stdio.h>
#include <math.h>
#include <string.h>

typedef struct danhSach {
	char ten[50];
	float cc;
	int cntc;
}DS[100];

void makeNULL(DS A, int* n) {
	*n = 0;
}

void display(DS A, int n) {
	for (int i = 1; i <= n; i++) {
		printf("%d %15s %7.2f %7d\n", i, A[i].ten, A[i].cc, A[i].cntc);
	}
}
void input(DS A, int* n) {
	for (int i = 1; i <= *n; i++) {
		printf("nhap ten: ");
		getchar();
		gets(A[i].ten);
		printf("nhap chieu cao: ");
		scanf("%f", &A[i].cc);
		A[i].cntc = A[i].cc * 100 - 105;
	}
}

void insert(DS A, int p, int* n) {
	char a[50];
	float b;
	int c;
	for (int i = *n; i >= p; i--)
		A[i+1] = A[i];
	printf("nhap ten: ");
	getchar();
	gets(a);
	printf("nhap chieu cao: ");
	scanf("%f", &b);
	c = b * 100 - 105;
	strcpy(A[p].ten, a);
	A[p].cc = b;
	A[p].cntc = c;
	(*n)++;
}
void delete(DS A, int p, int *n) {
	for (int i = p + 1; i <= *n; i++)
		A[i-1] = A[i];
	(*n)--;
}
int search(DS A, int n, char name[50]) {
	int found = 0;
	int pos;
	pos = 1;
	while (pos != n && found == 0)
		if (strcmp(A[pos].ten, name) == 0)
			found = 1;
		else pos++;
	return (pos == n) ? -1 : pos;
}
float max(DS A, int n) {
	int max = A[1].cc;
	for (int i = 2; i <= n; i++) {
		if (A[i].cc > max)
			max = A[i].cc;
	}
	return max;
}
int main() {
	DS list;
	int n;
	int select;
	while (1) {
		printf("\t\t\t\t\tmenu");
		printf("\n1.Nhap mot danh sach ");
		printf("\n2.Liet ke danh sach ");
		printf("\n3. Them vao danh sach");
		printf("\n4. Tim kiem ten trong danh sach");
		printf("\n5. Xoa vi tri bat ki trong danh sach");
		printf("\n6. Xoa ten thu n trong danh sach");
		printf("\n0. Ket thuc");
		printf("\n______________________________________________\n\n");
		int x;
		char name[50];
		printf("nhap lua cho cuar ban: ");
		scanf("%d", &select);
		switch (select)
		{
		case 1:
			makeNULL(list, &n);
			printf("nhap so luong sinh vien: ");
			scanf("%d", &n);
			input(list, &n);
			break;
		case 2:
			display(list, n);
			break;
		case 3:
			printf("nhap vi tri can them sinh vien: ");
			scanf("%d", &x);
			insert(list, x, &n);
			break;
		case 4:
			printf("Nhap ho ten can tim kiem: ");
			getchar();
			gets(name);
			x = search(list, n, name);
			if (x == -1)
				printf("ten sinh vien khong co trong danh sach \n");
			else
				printf("thong tin ca nhan nguoi vua tim\n %s %7.2f %7d\n", list[x].ten, list[x].cc, list[x].cntc);
			break;
		case 5:
			printf("nhap vi tri can xoa: ");
			scanf("%d", &x);
			delete(list, x, &n);
			break;
		case 6:
			printf("Nhap ho ten can xoa: ");
			getchar();
			gets(name);
			x = search(list, n, name);
			if (x == -1)
				printf("ten sinh vien khong co trong danh sach \n");
			else
				delete(list, x, &n);
			break;
		case 7:
			printf("nguoi co chieu cao lon nhat la: %f", max(list, n));	
		default:
			exit(1);
			break;
		}
	}
}
