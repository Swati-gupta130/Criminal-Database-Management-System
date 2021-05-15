# Criminal-Database-Management-System
#include <iostream.h>
#include<conio.h>
#include <fstream.h>
#include <stdio.h>
#include<string.h>
#include<dos.h>
#include<process.h>
class crim_rec
{
    char name[20], sex, fathr_name[20], addrs[25], offense[20], blood[5], dob[9];
    int crim_code, reward;
    void disp();
public:
    void get();
    void wtf();
    void rff();
    void search();
    void del();
    void mod();
}c;
void crim_rec::get()
{
    puts("\nEnter name of criminal:");
    gets(name);
    puts("\nsex (m/f):");
    cin>>sex;
    puts("\nEnter date of birth:");
    gets(dob);
    puts("Enter blood group (Ap/An/Bp/Bn/ABp/ABn/Op/On:");
    gets(blood);
    puts("\nenter father's name:");
    gets(fathr_name);
    puts("enter address:");
    gets(addrs);
    puts("\nEnter crime commited:");
    gets(offense);
    puts("\nEnter reward on criminal:");
    cin>>reward;
}
void crim_rec::disp()
{
    cout<<"The record of criminal:\n";
    cout<<"\nName of criminal: "<<name;
    cout<<"\nsex: "<<sex;
    cout<<"\nDOB: "<<dob;
    cout<<"\nBlood Group: "<<blood;
    cout<<"\nFather's name: "<<fathr_name;
    cout<<"\nAddress: "<<addrs;
    cout<<"\nCrime: "<<offense;
    cout<<"\nReward: "<<reward;
    
}
void crim_rec::wtf()
{
    ofstream ofile;
    ofile.open("CBI", ios::app);
    get();
    ofile.write((char*)&c, sizeof(c));
    ofile.close();
}
void crim_rec::rff()
{
    ifstream ifile;
    ifile.open("CBI");
    ifile.seekg(0, ios::beg);
    ifile.read((char*)&c, sizeof(c));
    while(ifile)
    {
        disp();
	ifile.read ((char*)&c, sizeof(c));
    }
    ifile.close();
}
void crim_rec::search()
{
    char m[20];
    ifstream ifile("CBI");
    puts("Enter name of criminal which has to be searched");
    gets(m);
    ifile.seekg (0, ios::beg);
    ifile.read((char*)&c, sizeof(c));
    while(ifile)
    {
	if (strcmpi(m, name)==0)
            disp();
	    ifile.read((char*)&c, sizeof(c));
    }
    ifile.close();
}
void crim_rec::del()
{
    char b[20];
    ifstream ifile;
    ifile.open("CBI", ios::app);
    ofstream ofile;
    ofile.open("new", ios::app);
    puts("Enter the name of the criminal whose records you want to del");
    gets(b);
    ifile.seekg (0, ios::beg);
    ifile.read((char*)&c, sizeof(c));
    while(ifile)
    {
        if (strcmpi(b, name))
	    ofile.write((char*)&c, sizeof(c));
        ifile.read((char*)&c, sizeof(c));
    }
    ifile.close();
    ofile.close();
    remove ("CBI");
    rename("new", "CBI");
}
void crim_rec::mod()
{
    char d[20];
    int p;
    puts("\nEnter name of criminal whose record you want to modify\n");
    gets(d);
    fstream f;
    f.open("CBI", ios::in|ios::out);
    f.seekg(0, ios::beg);
    f.read((char*)&c, sizeof(c));
    int a=f.tellg();
    while(! f.eof())
    {
        if (!strcmpi(d, name))
	{
            puts("\nPress 1 to change name\nPress 2 to change sex\nPress 3 to change date of birth\nPress 4 to change blood group\nPress 5 to change father's name\nPress 6 to change address\nPress 7 to change crime committed\nPress 8 to change reward on criminal\n");
            cin>>p;
            switch(p)
            {
	    case 1:

		gets(name);
		break;
	    case 2:

                cin>>sex;
                break;
	    case 3:

		gets(dob);
		break;
	    case 4:

		gets(blood);
		break;
	    case 5:
		clrscr();
		gets(fathr_name);
		break;
	    case 6:

		gets(addrs);
		break;
	    case 7:

		gets(offense);
		break;
	    case 8:

		cin>>reward;
		break;
            }
            f.seekg(a-sizeof(c), ios::beg);
            f.write((char*)&c, sizeof(c));
        }
	f.read((char*)&c, sizeof(c));
        a=f.tellg();
    }
    f.close();
}


void pass()
{
 clrscr();
 int m,k,i;
 char pass[20],user[40];
 cout<<"\n\n\n\t\tEnter Username: ";
 gets(user);
 cout<<"\n\t\tEnter Password: ";
 for(i=0;i<6;i++)
 {
  pass[i]=getch();
  cout<<"*";
 }
 pass[i]='\0';
 k=strcmp(pass,"nitish");
 m=strcmpi(user,"mukul");
 if(k==0&&m==0)
 {
  cout<<"\n\n\n\t\t\tLOGIN SUCCESS...... ";
  cout<<"\n\n\n\t\tPRESS ANY KEY TO START";
  getch();
 }
 else
 {
  cout<<"\nWRONG PASSWORD....\n\t\tEXITING.....";
  delay(1000);
  exit(10);
 }
}


void main ()
{
    clrscr();
    int ch;
    char choice;
  cout<<"\n\n\n\n\n\n\n\n";   //welcome screen
  cout<<"              **      :::::::  !!!!!!!!           \n";
  cout<<"           _____  **      ::       !!    !!         _____  \n";
  cout<<"                **      ::       !!    !!                \n";
  cout<<"              ******  :::::::  !!!!!!!!            \n";
    gotoxy(10,17);cout<<"Project By->MUKUL ANAND AND NITISH MANHAS";
    gotoxy(10,18);cout<<"~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~";
    gotoxy(5,22);cout<<"Press Any Key To Start";
    getch();
    clrscr();
    pass();
    clrscr();
    do
    {
    cout<<"\n\n\t\t\n";
    cout<<"\t\t....WELCOME TO THE CRIMINAL DATABASE SYSTEM....\n";
    cout<<"\t\t\n";
    cout<<"\t\t         \n";
    cout<<"\t\t MAIN MENU \n";
    cout<<"\t\t         \n";
    cout<<"\t Central Bureau of Investigation";
    cout<<"\n ********************************************";
    cout<<"\n\n *       1. View criminal details           *";
    cout<<"\n\n * 	2. Add new criminal details         *";
    cout<<"\n\n *  	3. Search a criminal record         *";
    cout<<"\n\n *  	4. Delete a criminal record         *";
    cout<<"\n\n * 	5. Modify a criminal record         *";
    cout<<"\n ********************************************";
    cout<<"\n\n Enter your choice: ";
    cin>>ch;

    clrscr();
    switch(ch)
    {
    case 1:
	     clrscr();
	     c.rff();
	break;
    case 2:
	    clrscr();
	    c.wtf();

	    break;
    case 3:
    clrscr();
	    c.search();
	    break;
    case 4:
    clrscr();
	c.del();
	break;
    case 5:
    clrscr();
	c.mod();
	break;
    default:
	{
	clrscr();
	cout<<"\nerror!";
	}
	break;
    }
    cout<<"\ncontinue? (y/n)\n";
    cin>>choice;
    clrscr();
    }while(choice=='y');
    cout<<"\nGood bye";

    getch();
}
