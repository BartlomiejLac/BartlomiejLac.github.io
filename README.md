**Hello!**  
Nazywam się Bartłomiej Łaciak, witaj na mojej stronie!

Studiuję obecnie Informatykę i Systemy Inteligentne na Akademii Górniczo Hutniczej w Krakowie [link](https://www.agh.edu.pl).

Pogłębiam swoją wiedzę w językach Python oraz C, tutaj przykładowy program:

```c
#include<stdio.h>
int main(void){
int mx,my,k,l,w;
while (ocena(pl)==0){
wypisz(pl);
best(pl,8,&mx,&my);
pl[mx][my]='x';
printf("Komputer wykonal ruch na %d,%d\n",mx+1,my+1);
wypisz(pl);
if (pelne(pl)==1) {printf("Remis\n"); break;}
int wykonano=0;
if (ocena(pl)==0){
while (wykonano==0){
printf("Wpisz wlasciwe wspolrzedne ruchu ");
char input[5];
scanf("%s",&input);
w=sscanf(input, "%d,%d",&k,&l);
if (w==2 && k<4 && k>0 && l<4 && l>0){
if (pl[k-1][l-1]==' ') {pl[k-1][l-1]='o'; wykonano=1;}}}}
}
if (ocena(pl)==99) printf("Przegrales\n");
if (ocena(pl)==-99) printf("Wygrales\n");}

int ocena(char plansza[3][3]){
for (int x=0;x<3;x++){
if (plansza[x][0]=='x') {
if (plansza[x][1]=='x' && plansza[x][2]=='x') return 99;}
if (plansza[0][x]=='x') {
if (plansza[1][x]=='x' && plansza[2][x]=='x') return 99;}
if (plansza[0][0]=='x' && plansza[1][1]=='x' && plansza[2][2]=='x') return 99;
if (plansza[2][0]=='x' && plansza[1][1]=='x' && plansza[0][2]=='x') return 99;}
for (int x=0;x<3;x++){
if (plansza[x][0]=='o') {
if (plansza[x][1]=='o' && plansza[x][2]=='o') return -99;}
if (plansza[0][x]=='o') {
if (plansza[1][x]=='o' && plansza[2][x]=='o') return -99;}
if (plansza[0][0]=='o' && plansza[1][1]=='o' && plansza[2][2]=='o') return -99;
if (plansza[2][0]=='o' && plansza[1][1]=='o' && plansza[0][2]=='o') return -99;}
return 0;}

int wypisz(char plansza[3][3]){
for (int f=0;f<3;f++){
for (int g=0;g<3;g++){
if (g==2) printf("%c\n",plansza[f][g]);
else printf("%c|",plansza[f][g]);}}
return 0;}

int pelne(char plansza[3][3]){
for (int a=0;a<3;a++){
for (int b=0;b<3;b++){
if (plansza[a][b]==' ') return 0;
}}
return 1;
}

int best(char plansza[3][3], int depth, int *rx, int *ry){
int wynik,wynikmax,wynikmin,a,b;
wynik=depth*ocena(plansza);
wynikmax=-1000;
wynikmin=1000;
if (wynik!=0 || depth==0) return wynik;
if (pelne(plansza)==1) return 0;
if (depth%2==0){
    for (int x=0; x<3; x++){
        for (int y=0; y<3; y++){
            if (plansza[x][y]==' '){
                plansza[x][y]='x';
                wynik=best(plansza, depth-1, &a, &b);
                plansza[x][y]=' ';
                if (wynik>wynikmax) {wynikmax=wynik; *rx=x; *ry=y;}
            }
            }
        }
 return wynikmax;}
 if (depth%2==1){
    for (int x=0; x<3; x++){
        for (int y=0; y<3; y++){
            if (plansza[x][y]==' '){
                plansza[x][y]='o';
                wynik=best(plansza, depth-1, &a, &b);
                plansza[x][y]=' ';
                if (wynik<wynikmin) {wynikmin=wynik;}
            }
        }
    }
 return wynikmin;}
}
```
