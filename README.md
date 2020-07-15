# projectc-

#include <iostream>
#include <string.h>
#include <fstream>

using namespace std;

class persinfo
{
protected:
int rno;
char name[20];
char address[100];

public:
persinfo()
  {
  rno = 0;
  strcpy(name,"\o");
  strcpy(address,"\o");
  }
persinfo(int r, char* n, char* a)
  {
  rno = r;
  strcpy(name,n);
  strcpy(address,a);
  }
void getdata()
  {
  cout<<"Enter roll number"<<endl;
  cin>>rno;
  cout<<"Enter Name"<<endl;
  cin>>name;
  cout<<"Enter address"<<endl;
  cin.getline(address, '/n');
  }
};

class batchinfo
{
protected:
int batch_no;
char batch _name[20];
float duration;
float cost;

public:
batchinfo()
  {
  batch_no = 0;
  strcpy(batch_name, "\o");
  duration = 0.0;
  cost = 0.0;
  }
batchinfo(int b, char* nam, float d, float c)
  {
  batch_no = b;
  strcpy(batch_name, nam);
  duration = d;
  cost = c;
  }
void getdata()
  {
  cout<<"Enter batch number"<<endl;
  cin>>batch_no;
  cout<<"Enter batch name"<<endl;
  cin>>batch_name;
  cout<<"Enter duration"<<endl;
  cin>>duration;
  cout<<"Enter cost"<<endl;
  cin>>cost;
  }
};

class student: private persinfo, private batchinfo
{
private:
float trans_amt;
float pending_amt;
static int tot;

public:
student(): persinfo(), batchinfo()
  {
  trans_amt = 0.0;
  pending_amt = 0.0;
  }
student(float t, int r, char* n, char* a, int b, char* num, float d, float c):
persinfo(r,n,a), batchinfo(b,nam,d,c)
  {
  trans_amt = t;
  pending_amt = c-t;
  }

void getdata()
  {
  persinfo::getdata();
  batchinfo::getdata();
  cout<<"Enter transaction amount";
  cin>>trans_amt;
  pending_amt = cost - trans_amt;
  }
  
 void dispdata()
  {
  tot = tot + trans_amt;
  cout<<endl<<rno<<"\t";
  cout<<"\t"<<name;
  cout<<"\t"<<batch_no<<"\t";
  cout<<"\t"<<trans_amt;
  }
static void pl()
  {
  cout<<"Total"<<"\t\t\t\t\t\t"<<tot;
  }
};

int student::tot = 0;

int main()
{
int choice;
void add();
void display();

do
  {
  cout<<"\n1. Add";
  cout<<"\n2. Display";
  cout<<"\n3. Quit";
  cout<<"\nEnter choice";
  cin>>choice;
  
  switch(choice)
    {
	case1: add()
	break;
	
	case2: display();
	break;
	
	case3: break;
	}
  }
  
while(choice != 3);
}

void add()
{
student s1;
fstream stdfile;
stdfile.open("xyz.dat", ios::out| ios::binary)
char wish;

do
  {
  s1.getdata();
  stdfile.write((char*)&s1, sizeof(student));
  cout<<"Continue?";
  cin>>wish;
  }
while(wish == 'y'||wish =='Y');
stdfile.close;
}

void display()
{
student s1;
fstream stdfile;
stdfile.open("xyz.dat", ios::in| ios::binary)
stdfile.read((char*)&s1, sizeof(student));
cout<<"STUDENT REPORT"<<endl;
cout<<"Roll Number\t";
cout<<"Name\t";
cout<<"Batch number\t";
cout<<"Transaction amount\t";
while(stdfile)
  {
  s1.dispdata();
  stdfile.read((char*)&s1, sizeof(student));
  }
student::pl();
stdfile.close();
}