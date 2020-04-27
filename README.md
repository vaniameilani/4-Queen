# 4-Queen-CSP

CSV (Constraint Satisfaction Problem) adalah suatu permasalahan yang tujuannya adalah mendapatkan suatu kombinasi variabel-variabel tertentu yang memenuhi aturan-aturan tertentu.
Untuk kali, permasalahan yang akan dibahas adalah 4-queen.
Pembahasan programnya adalah sebagai berikut  :
1. Pada fungsi utama , mendeklarasikan terlebih dahulu letak awal pada Queen yaitu `board[N][N]={0};`, kemudian memanggil pada fungsi `Solve`, dimana  
untuk mencari kemungkinan kotak yang tepat dan aman. Jika setelah penelusurun dilakukan, maka diguanakan metode Backtracking.
Fungsi tersebut yaitu : 
```
void Solve(int row){
	if(row == N+1){
		Print();
		cin.get();
		return;
	}
	for(int i = 1; i <= N; i++){
		if(board[row][i] == 0){
			area(row, i, 0, row);
			bool place = false;
			for(int j = row + 1; j <= N; j++){
				place = true;
				for(int k = 1; k <= N; k++){
					if(board[j][k]==0){
						place = false;
					}
				}
				if(place) break;
			}
			if(!place) Solve(row+1);
			area(row, i, row, 0);
		}
	}
}
```
2. Terapat pemanggilan fungsi `area` yang berfungsi untuk menandai area/kotak yang telah diduduki oleh Queen
```
void area(int row, int t, int inisial, int mrow){
	int i;
	board[row][t] = mrow;
	for(i = row; i <= N; i++)
		if(t-(i-row) > 0){
			if(board[i][t-(i-row)] == inisial) board[i][t-(i-row)] = mrow;
		}
		if(board[i][t] == inisial) board[i][t] = mrow;
		if(t+(i-row) < N+2){
			if(board[i][t+(i-row)] == inisial) board[i][t+(i-row)] = mrow;
		}
	}
}
```
3. Fungsi untuk print output
```
void Print(){
	int i, j;
	printf("Solusi %d:\n", solusi);
	solusi++;
	for(i = 1; i <= N; i++){
		for(j = 1; j <= N; j++){
			if(board[i][j] == i){
				printf("1 ");
			}
			else printf("0 ");
		}
		printf("\n");
	}
}
```
