include<stdio.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>
struct person
{
    char name[35];
    char address[50];
    char father_name[35];
    char disease_name[30];
    long int mble_no;
    float totalfee;
	float paid;
	float pending;
    };
void menu();
void got();
void start();
void back();
void addrecord();
void listrecord();

int main()
{
    start();
    return 0;
}
void back()
{
    start();
}
void start()
{
    menu();
}
void menu()
{
printf(" WELCOME TO MEDICAL RECORD\n");

printf("MENU\n");
printf("1.Add New \n2.List \n3.Exit\n  ");

switch(getch())
{
    case '1':
    addrecord();
    break;
   case '2': listrecord();
    break;
    case '3': exit(0);
    break;
    default:
                printf("\nEnter 1 to 3 only");
                printf("\n Enter Any Key");
                getch();

menu();
}
}
        void addrecord()
{
        system("cls");
        FILE *f;
        struct person p;
        f=fopen("project","ab+");
        printf("\nEnter Name: ");
        got(p.name);
        printf("\nEnter Address: ");
        got(p.address);
        printf("\nEnter Father Name: ");
        got(p.father_name);
        printf("\nEnter Disease Name: ");
        got(p.disease_name);
        printf("\nEnter Phone Number: ");
        scanf("%ld",&p.mble_no);
        printf("\nEnter Totalfee:");
        scanf("%f",&p.totalfee);
        printf("\nEnter Paid:");
        scanf("%f",&p.paid);
        p.pending=p.totalfee-p.paid;
        fwrite(&p,sizeof(p),1,f);
      fflush(stdin);
        printf("\nRecord Saved !!");

fclose(f);

    printf("\n\nEnter Any Key");

     getch();
    menu();
}
void listrecord()
{
    struct person p;
    FILE *f;
f=fopen("project","rb");
if(f==NULL)
{
printf("\nFile Opening Error In Listing :");

exit(1);
}
while(fread(&p,sizeof(p),1,f)==1)
{
     printf("\n\n\n YOUR RECORD IS\n\n ");
        printf("\nName: %s\nAdress: %s\nFather Name: %s\nDisease Name: %s\nMobile Number: %ld\nTotal fee:%.2f\nPaid :%.2f\nPending :%.2f",p.name,p.address,p.father_name,p.disease_name,p.mble_no,p.totalfee,p.paid,p.pending);

     getch();
     system("cls");
}
fclose(f);
 printf("\nEnter Any Key");
 getch();
menu();
}

void got(char *name)
{

   int i=0,j;
    char c,ch;
    do
    {
        c=getch();
                if(c!=8&&c!=13)
                {
                    *(name+i)=c;
                        putch(c);
                        i++;
                }
                if(c==8)
                {
                    if(i>0)
                    {
                        i--;
                    }
                    for(j=0;j<i;j++)
                    {
                        ch=*(name+j);
                        putch(ch);

                    }

                }
    }while(c!=13);
      *(name+i)='\0';
}
