**Hello** :wave: Nazywam się Bartłomiej Łaciak, witaj na mojej stronie!

Studiuję obecnie Informatykę i Systemy Inteligentne na Akademii Górniczo Hutniczej w Krakowie [link](https://www.agh.edu.pl).

Pogłębiam swoją wiedzę w językach Python oraz C, tutaj przykładowy program:

```c
#include<stdio.h>
int main(void){
int rx=0,ry=0,k,l;
char pl[10][10]={{' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '},
                {' ',' ',' ',' ',' ',' ',' ',' ',' ',' '}};
wypisz(pl);
while (opps(pl)!=5 && threats(pl)!=5){
printf("%d\n",opps(pl));
printf("%d\n",threats(pl));
best(pl, 4, &rx, &ry);
pl[rx][ry]='x';
printf("Komputer wykonal ruch na %d %d\n",rx+1,ry+1);
wypisz(pl);
if (opps(pl)!=5 && threats(pl)!=5){
int w=0,wykonano=0;
while (wykonano==0){
printf("Wpisz wlasciwe wspolrzedne ruchu ");
char input[5];
scanf("%s",&input);
w=sscanf(input, "%d,%d",&k,&l);
if (w==2 && k<11 && k>0 && l<11 && l>0){
if (pl[k-1][l-1]==' ') {pl[k-1][l-1]='o'; wykonano=1;}}}}
wypisz(pl);
}
if (opps(pl)==5) printf("Przegrales\n");
if (threats(pl)==5) printf("Wygrales\n");
return 0;}

int opps(char plansza[10][10]){
int punktymax=0,punkty=0;
for (int x=0;x<10;x++){
for (int y=0;y<10;y++){
if (plansza[x][y]=='x'){
punkty++;
for (int a=1;a<5 && y+a<10;a++){
if (plansza[x][y+a]=='x') punkty++;
if (plansza[x][y+a]=='o') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
for (int x=0;x<10;x++){
for (int y=0;y<10;y++){
if (plansza[y][x]=='x'){
punkty++;
for (int a=1;a<5 && y+a<10;a++){
if (plansza[y+a][x]=='x') punkty++;
if (plansza[y+a][x]=='o') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
for(int x=0;x<10;x++){
for(int y=0;y<10;y++){
if (plansza[x][y]=='x') {
punkty++;
for(int a=1;a<5 && y+a<10 && x+a<10;a++){
if (plansza[x+a][y+a]=='x') punkty++;
if (plansza[x+a][y+a]=='o') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=1;
for(int a=1;a<5 && y-a>=0 && x+a>=0;a++){
if (plansza[x+a][y-a]=='x') punkty++;
if (plansza[x+a][y-a]=='o') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
return punktymax;}

int threats(char plansza[10][10]){
int punktymax=0,punkty=0;
for (int x=0;x<10;x++){
for (int y=0;y<10;y++){
if (plansza[x][y]=='o'){
punkty++;
for (int a=1;a<5 && y+a<10;a++){
if (plansza[x][y+a]=='o') punkty++;
if (plansza[x][y+a]=='x') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
for (int x=0;x<10;x++){
for (int y=0;y<10;y++){
if (plansza[y][x]=='o'){
punkty++;
for (int a=1;a<5 && y+a<10;a++){
if (plansza[y+a][x]=='o') punkty++;
if (plansza[y+a][x]=='x') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
for(int x=0;x<10;x++){
for(int y=0;y<10;y++){
if (plansza[x][y]=='o') {
punkty++;
for(int a=1;a<5 && y+a<10 && x+a<10;a++){
if (plansza[x+a][y+a]=='o') punkty++;
if (plansza[x+a][y+a]=='x') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=1;
for(int a=1;a<5 && y-a>=0 && x+a>=0;a++){
if (plansza[x+a][y-a]=='o') punkty++;
if (plansza[x+a][y-a]=='x') break;}
if (punkty>punktymax) punktymax=punkty;
punkty=0;
}}}
return punktymax;}

int wypisz(char plansza[10][10]){
for (int f=0;f<10;f++){
for (int g=0;g<10;g++){
if (g==9) printf("%c\n",plansza[f][g]);
else printf("%c|",plansza[f][g]);}}
return 0;}

int best(char plansza[10][10], int depth, int *rx, int *ry){
int wynik,wynikmax,wynikmin,a,b;
if (opps(plansza)>=threats(plansza)) wynik=opps(plansza)*10+depth;
if (opps(plansza)<threats(plansza)) wynik=-10*threats(plansza)-depth;
wynikmax=-100;
wynikmin=100;
if (threats(plansza)==5 || opps(plansza)==5 || depth==0) return wynik;
if (pelne(plansza)==1) return 0;
if (depth%2==0){
    for (int x=0; x<10; x++){
        for (int y=0; y<10; y++){
            if (plansza[x][y]==' ' && blisko(plansza,x,y)==1){
                plansza[x][y]='x';
                wynik=best(plansza, depth-1, &a, &b);
                plansza[x][y]=' ';
                if (wynik>wynikmax) {wynikmax=wynik; *rx=x; *ry=y;}
            }
        }
    }
 return wynikmax;}
 if (depth%2==1){
    for (int x=0; x<10; x++){
        for (int y=0; y<10; y++){
            if (plansza[x][y]==' ' && blisko(plansza,x,y)==1){
                plansza[x][y]='o';
                wynik=best(plansza, depth-1, &a, &b);
                plansza[x][y]=' ';
                if (wynik<wynikmin) {wynikmin=wynik;}
            }
        }
    }
 return wynikmin;}
}

int pelne(char plansza[10][10]){
for (int a=0;a<10;a++){
for (int b=0;b<10;b++){
if (plansza[a][b]==' ') return 0;
}}
return 1;
}

int blisko(char plansza[10][10], int x, int y){
for (int i=-1; i<2; i++){
    for(int f=-1; f<2; f++){
        if (x+i>=0 && x+i<10 && y+f>=0 && y+f<10 && plansza[x+i][y+f]!=' ') return 1;
    }
}
return 0;
}
```
