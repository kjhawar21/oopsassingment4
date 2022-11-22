# oopsassingment4
/*This program is a mock representation of a working of Mc Donalds. There are Part Time Emplyoee who add details of customers and Regular emplyoee who add attendace of Part time employee and for the head to calculate salary of all the employee
*/
#include <iostream>
#include <cstring>
using namespace std;
int sumreg,sumpart;
char dcus[100][20];
int nc=0,d[100];
//Template
template <class T>
void sort(T a[],int n)
{
    T x;
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = n - 1; i < j; j--)
        {
            if (a[j] < a[j - 1])
            {
                x=a[j];
                a[j]=a[j-1];
                a[j-1]=x;
            }
        }
    }
}
class Employee
{
public:
    char name[20];
    int id;
    double salary;
    double DA, HRA, basic;
    int number_of_hours;
    double pay_per_hour;
    void get_data()
    {
        cout << "Enter the name : ";
        cin.get();
        cin.getline(name, 20);
        cout << "Enter the id : ";
        cin >> id;
    }
    void input()
    {
        cout << "Enter the basic salary : ";
        cin >> basic;
        cout << "Enter DA and HRA : ";
        cin >> DA >> HRA;
    }
    void part_time()
    {
        cout << "Enter the number of hours : ";
        cin >> number_of_hours;
        cout << "Enter the salary per hour : ";
        cin >> pay_per_hour;
    }
    //Virtual Function
    virtual void display() = 0;
};
void s_reg(){
    
}
//Inhertance
class Regular : public Employee
{
public:
    void display()
    {
        cout<<"Name : "<<name<<endl;
        cout<<"ID : "<<id<<endl;
        cout << "Salary : " << (DA + HRA + basic);
        sumreg=DA + HRA + basic;
        cout << endl;
    }
};
class PartTime : public Employee
{
public:
    void display()
    {
        cout<<"Name : "<<name<<endl;
        cout<<"ID : "<<id<<endl;
        cout << "\nSalary : " << (number_of_hours * pay_per_hour);
        sumpart=number_of_hours * pay_per_hour;
    }
};
class Fin{
    public:
    int part,reg;
    void input_part(int a){
    part=a;
    }
 void input_reg(int a){
    reg=a;
    }
    Fin operator+(Fin a){
        Fin sum;
        sum.part=a.part+part;
        sum.reg=a.reg+reg;
        return sum;
    }
};
 class customer{
    private:
    int amt;
    public:
   customer();
   ~customer();
   //Friend Function
    friend void inputt(customer &o);
    
 };
 //Scope Resolution + Cunstructor and Destructor
 customer:: customer(){
        cout<<"Constructor Called";
        amt=0;
    }
 customer:: ~customer(){
        cout<<"Destructor Called";
    }
 void inputt(customer &o){
    cout<<"Enter the name of the customer: ";
    cin>>dcus[nc], 20;
    cout<<"Enter the amount: \n";
    cin>>o.amt;
    d[nc]=o.amt;
    nc++;
 }
 void displayy(){
    cout<<"The number of customers that came today : "<< nc<<endl;
    cout<<"The list of past customers are and amt paid: \n";
    for(int i=0;i<nc;i++)
    cout<<dcus[i]<<" "<<d[i]<<"$"<<endl;
 }
int main()
{
    int in=0,fn=0,i[100];
    float f[100];
    float cho;
    do{
    cout<<"Press 1 if u are a Regualar emplyoee \n";
    cout<<"Press 2 if u are a Part Time emplyoee \n";
    cout<<"Press 3 to Money to be paid to the employee \n";
    cout<<"Press 4 to enter the details of the customer\n ";
    cout<<"Press 4.5 to enter the review of the customer\n";
    cout<<"Press 5 to enter the charity amt of previous customers\n";
    cout<<"Press 6 to have list of customers that visited today\n";
    cout<<"Press 7 System Space Check\n ";
    cout<<"Press 0 to shut Down \n";    
    cin>>cho;
    if(cho==1){
    cout << "Regular employee" << endl;
    Regular r;
    Employee *sr = &r;
    sr->get_data();
    sr->input();
    cout << "\nDetails of Regular employee" << endl;
    sr->display();
    }
    else if(cho==2){
    
    cout << "Part time employee" << endl;
    PartTime p;
    Employee *sp = &p;
    sp->get_data();
    sp->part_time();
    
    cout << "\nDetails of Part time employee" << endl;
    sp->display();
    
    }
    else if(cho==3){
    Fin a;
    Fin b;
    int pa,re;
     a.input_part(sumpart);
     cout<<"Enter the salary of other employee \n";
     cin>>pa;
     a.input_part(pa);
     b.input_reg(sumreg);
     cout<<"Enter the salary of other employee \n";
     cin>>re;
     b.input_reg(re);
     Fin c;
     c=a+b;
     cout<<"The salary for Part Time Employee: "<<c.part<<endl;
     cout<<"The salary for Regular Employee: "<<c.reg;
    }
    else if(cho==4){
    customer a;
    inputt(a);
    }
    else if(cho==5){
      cout <<"Enter number of customers that gave charity ";
      cin>>fn;
      cout<<"Enter the amount collected from the customers for charity\n"<<endl;
      
    for(int a=0;a<fn;a++)
    {
        cout<<"Enter f["<<a<<"]:";
        cin>>f[a];
    }
    sort<float>(f,fn);
    cout << " Sorted list from smallest to largest amount submitted : ";
    for (int n = 0; n < fn; n++)
        cout << f[n] << " ";
    cout << endl;
    }
    else if(cho==6){
       displayy();
    }
    else if(cho==7){
        if(nc<100)
        cout<<"You can store data of "<<100-nc<<" new customers.";
        else
        cout<<"System space for customer is full!!";
    }
    else if(cho==4.5){
    int a=in; 
    cout<<"Enter the total number of a customer \n ";
    cin>>in;
    cout<<"Enter all the review of the customers \n ";
    fn=in; 
    for(;a<in;a++)
    {
        cout<<"Enter i["<<a<<"]:";      
        cin>>i[a];
    }
    sort<int>(i,in);
    cout << " Sorted array reviews : ";
    for ( int n=0; n < in; a++)
        cout << i[n] << " ";
    cout << endl;
    }
       }while(cho!=0);
    return 0;
}
