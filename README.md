# Hungry-snake
A very ordinary game
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
#include<iso646.h>
#include<windows.h>
#include<time.h>
#define X 70
#define Y 30
void init();
void map();
void printsnake();
void snakemove();
void printfood();
void printpoi();
void printNAN();
void whetherfood();
void whetherpoi();
void whetherNAN();
void ifhitwallOReatself();
void over();
void gotoxy(int x,int y);
struct snake {
	int x;
	int y;
	struct snake *next;
	struct snake *form;
};
struct snake *head;
struct snake *tail;
struct snake *q;
struct snake *ip;
int x,y,j,k,m,n,score;
float speed;
int main(void) {
	init();
	map();
	printsnake();
	snakemove();
	over();
	return 0;
}
void init() {
	printf("\n\n\n\n\n\n\n              Do you like van♂游戏?\n\n\n");
	printf(".                    please hit the keyboard with your \
head to start the game\n");
	printf("\n\n\n\n\n\n\n\nThe game is programmed by the \
wellknown zouYC.");
	while(!kbhit()) {
		;
	}
	system("cls");
}
void map() {
	printfood();
	printpoi();
	printNAN();
	int x,y;
	for(y=1; y<=Y; y++) {
		if(y==1 or y==Y) {
			for(x=1; x<=X; x++) {
				gotoxy(x,y);
				printf("#");
			}
		} else {
			for(x=1; x<=X; x++) {
				if(x==1 or x==X) {
					gotoxy(x,y);
					printf("#");
				}
			}
		}
	}
	int score=0;
	gotoxy(X+3,Y/2-2);
	printf("你的分数：%d",score);
	gotoxy(X+3,Y/2+2);
	printf("特殊说明：当贪吃蛇吃掉♂\
时，会变得更加亢♂奋！");
}

void printfood() {
	int m,n;
	srand((unsigned)time(NULL));
	m=rand()%(X-1)-1;
	n=rand()%(Y-1)-1;
	gotoxy(m,n);
	printf("€");
}
void printpoi() {
	int j,k;
	srand((unsigned)time(NULL));
	j=rand()%(X-1)-1;
	k=rand()%(Y-1)-1;
	gotoxy(j,k);
	printf("?");
}
void printNAN() {
	int r,t;
	srand((unsigned)time(NULL));
	r=rand()%(X-1)-1;
	t=rand()%(Y-1)-1;
	gotoxy(r,t);
	printf("♂");
}
void printsnake() {

	int body=5;
	struct snake *tail=
	    (struct snake *)malloc(sizeof(struct snake));
	tail->x=X/7+1;
	tail->y=Y/3+1;
	tail->next=NULL;
	tail->form=NULL;
	int i;
	for(i=1; i<=body; i++) {
		struct snake *body=
		    (struct snake *)malloc(sizeof(struct snake));
		body->x=tail->x-1;
		body->y=tail->y;
		body->next=tail;
		tail->form=body;
		tail=body;
	}
	struct snake *q=(struct snake *)malloc(sizeof(struct snake));
	q=tail;
	for(i=1; i<=body; i++) {
		gotoxy(q->x,q->y);
		printf("@");
		q=q->next;
	}
	struct snake *head=(struct snake *)malloc(sizeof(struct snake));
	head=q;
}
void snakemove() {
	char ch;
	while(1) {
		struct snake *ip=
		    (struct snake *)malloc(sizeof(struct snake));
		struct snake *newhead=
		    (struct snake *)malloc(sizeof(struct snake));
		if(_kbhit()) {
			ch=_getch();
		}
		switch(ch) {
			case 'w':

				head->next=newhead;
				newhead->x=q->x;
				newhead->y=q->y-1;
				newhead->next=NULL;
				newhead->form=head;
				head=newhead;
				whetherfood();

				break;

			case 'a':

				head->next=newhead;
				newhead->x=q->x-1;
				newhead->y=q->y;
				newhead->next=NULL;
				newhead->form=head;
				head=newhead;
				whetherfood();

				break;

			case 's':

				head->next=newhead;
				newhead->x=q->x;
				newhead->y=q->y+1;
				newhead->next=NULL;
				newhead->form=head;
				head=newhead;
				whetherfood();

				break;

			case 'd':

				head->next=newhead;
				newhead->x=q->x+1;
				newhead->y=q->y;
				newhead->next=NULL;
				newhead->form=head;
				head=newhead;
				whetherfood();

				break;

		}
		whetherpoi();
		whetherNAN();
		ifhitwallOReatself();
		while(q->next!=NULL) {
			gotoxy(q->x,q->y);
			printf("@");
			q=q->next;
		}
		Sleep(250-speed);
		gotoxy(X+3,Y/2-2);
		printf("你的分数：%d",score);
	}
}
void whetherfood() {
	if(head->x==m && head->y==n) {
		int m,n;
		srand((unsigned)time(NULL));
		m=rand()%(X-1)-1;
		n=rand()%(Y-1)-1;
		gotoxy(m,n);
		printf("€");
		score+=100;
	} else {
		gotoxy(tail->x,tail->y);
		printf(" ");
		ip=tail;
		tail=tail->next;
		tail->form=NULL;
		free(ip);
		q=tail;
	}
}
void whetherpoi() {
	if(head->x==j && head->==k) {
		gotoxy(tail->x,tail->y);
		printf(" ");
		ip=tail;
		tail=tail->next;
		tail->form=NULL;
		free(ip);
		q=tail;
		score-=50;
	}
}
void whetherNAN() {
	if(head->x==r && head->y==t) {
		int r,t;
		srand((unsigned)time(NULL));
		r=rand()%(X-1)-1;
		t=rand()%(Y-1)-1;
		gotoxy(r,t);
		printf("♂");
		score+=200;
		speed+=12.5;
	}
}
void ifhitwallOReatself() {
	int Life=0;
	if(head->x==1 or head->x==X or head->y==1 or
	        head->y==Y)
		life=1;
	struct snake *q=
	    (struct snake *)malloc(sizeof(struct snake));
	q=head->form;
	for(; q->form!=NULL; q=q->form) {
		if(q->x==head->x and q->y==head->y)
			Life=1
		}
	if(Life==1)
		break;
}
void over() {
	while(1)
		printf("game over                                game over \n");
}
void gotoxy(int x, int y) {
	COORD pos = {x,y};
	HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleCursorPosition(hOut, pos);
}



