/*
Final Copy of Program
*/
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
#include <ctime>
using namespace std;

///Global variables
ofstream fout;
ifstream fin;
char char_temp;
int int_temp;
string string_temp;
time_t t = time(0);   // get time now
tm* now = localtime(&t); ///Get date now


int i,j,max,arr[50],n,flag=0,len;
class hotel
{
    int customer_id_no,check_in_date,check_out_date;
    unsigned long long  contact_no;
    string customer_name,customer_location;
    char room_type,break_fast_service,guide_needed;

public:
    void set()
    {
        cout << "Enter customer name \n";
        again1:
        cin >> customer_name;
        len = customer_name.size();
        for(j=0;j<len;j++)
        {
            if(customer_name[j]=='*' || customer_name[j]=='?' || customer_name[j]=='[' || customer_name[j]==']' || customer_name[j]=='!' || customer_name[j]=='-' || customer_name[j]=='#')
            {
                cout << "Wild Card Characters are not allowed \n";
                goto again1;
            }
            else if( customer_name[j]>=48 && customer_name[j]<=57)
            {
                cout << "Numeric characters are not allowed \n";
                goto again1;
            }
            else if(!(customer_name[j]>=65&& customer_name[j]<=90|| customer_name[j]>=97&& customer_name[j]<=122))
            {
                cout << "Enter a valid character \nTry again \n";
                goto again1;
            }
        }

        cout << "Enter customer id \n";
        cin >> customer_id_no;


        cout << "Enter room type(Delux 'd' or classic 'c' )\n";
        again3:
        cin >> room_type;
        if(!(room_type=='d' || room_type=='D' || room_type=='c' || room_type=='C'  ))
        {
            cout << "Enter valid character \nTry again \n";
            goto again3;
        }

        cout << "Do you want breakfast(yes 'y' or no 'n') \n";
        again4:
        cin >> break_fast_service;
        if(!(break_fast_service=='y' || break_fast_service=='Y' || break_fast_service=='n' || break_fast_service=='N'  ))
        {
            cout << "Enter valid character \nTry again \n";
            goto again4;
        }


        cout << "Enter customer location \n";
        again5:
        cin >> customer_location;
        len  = customer_location.size();
        for(j=0;j<len;j++)
        {
            if( customer_location[j]>=48 && customer_location[j]<=57)
            {
                cout << "Numeric characters are not allowed \n";
                goto again5;
            }
        }
        cout << "Enter contact number \n";
        cin >> contact_no;

        cout << "Enter check in date \n";
        cin >> check_in_date;

        cout << "Enter check out date \n";
        cin >> check_out_date;

        cout << "Do you want guide(yes 'y' or no 'n') \n";
        again9:
        cin >> guide_needed;
        if(!(guide_needed=='y' || guide_needed=='Y' || guide_needed=='N' || guide_needed=='n'  ))
        {
            cout << "Enter valid character \nTry again \n";
            goto again9;
        }

        cout << "\nEntry completed \n";
    }

    void display()
    {
        cout << endl;
        cout << "\t\t**********************************************************************************\n";
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Name is "; cout << ":";               cout.setf(ios::left,ios::adjustfield);cout.width(10); cout  << customer_name << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Customer ID "; cout << ":";           cout.width(10); cout   << customer_id_no << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Room type "; cout << ":";             cout.width(10); cout  << room_type << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Guide Needed ";  cout << ":";         cout.width(10); cout  << guide_needed << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Breakfast needed "; cout << ":";      cout.width(10); cout  << break_fast_service << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Location ";  cout << ":";             cout.width(10); cout  << customer_location << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Contact Number "; cout << ":";        cout.width(10); cout  << contact_no << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Enter check in date "; cout << ":";   cout.width(10); cout  << check_in_date << endl;
        cout << "\t\t\t\t*"; cout.width(20); cout.setf(ios::left,ios::adjustfield); cout << "Enter check out date ";  cout << ":"; cout.width(10); cout  << check_out_date << endl;
        cout << "\t\t**********************************************************************************\n";
        cout << endl;
    }

    int get_id()
    {
        return customer_id_no;
    }

    int get_check_in_date()
    {
        return check_in_date;
    }
    int get_check_out_date()
    {
        return check_out_date;
    }

    string get_name()
    {
        return customer_name;
    }

    string get_location()
    {
        return customer_location;
    }

    char get_room_type()
    {
        return room_type;
    }

    char get_breakfast_service()
    {
        return break_fast_service;
    }

    char get_guide_needed()
    {
        return guide_needed;
    }

};

hotel obj[10];
///All the cases are solved here

void case1()
{

    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            if(obj[i].get_room_type()=='d'||obj[i].get_room_type()=='D')
            {
                cout << obj[i].get_name() << endl;
            }
    }
    fin.close();

}

void case2()
{

    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            if(obj[i].get_check_out_date()==now->tm_mday)
            {
                cout << obj[i].get_name() << endl;
            }
    }
    fin.close();

}

void case3()
{
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            if(obj[i].get_breakfast_service()=='y'||obj[i].get_breakfast_service()=='Y')
            {
                cout << obj[i].get_name() << endl;
            }
    }
    fin.close();
}

void case4()
{
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            string_temp = obj[i].get_name();
            if(string_temp.at(0)=='s'||string_temp.at(0)=='S')
            {
                cout << obj[i].get_name() << endl;
                flag++;
            }
    }
    if(flag==0)
            {
                cout << "No customer with name s \n";
            }
    fin.close();
}

void case5()
{
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            //if((strcmp(obj[i].get_location(),'ahmedabad')||obj[i].get_location(),'Ahmedabad')==0)
            if(obj[i].get_location()=="ahmedabad")
            {
                obj[i].display();
            }
    }
    fin.close();
}

void case6()
{

    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
            if((obj[i].get_check_out_date()==now->tm_mday)&&obj[i].get_guide_needed()=='y'||obj[i].get_guide_needed()=='Y')
            {
                cout << obj[i].get_name() << endl;
            }
    }
    fin.close();

}

void case7()
{
    cout << "Delux type customers\n";
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));

            if(obj[i].get_room_type()=='d'||obj[i].get_room_type()=='D')
            {
                cout << obj[i].get_name() << endl;
            }
    }
    fin.close();

    cout << "Classic type customers \n";
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));

            if(obj[i].get_room_type()=='C'||obj[i].get_room_type()=='c')
            {
                obj[i].display();
            }
    }
    fin.close();
}

void case8()
{
            /*
            --> Storing the dates of all the customers in an array
            --> Sorting them in descending order
            --> display them according to their name
            */

    ///Storing the dates in an array
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
        arr[i]=obj[i].get_check_in_date();
    }
    fin.close();

    ///Sorting them in ascending order
    for(i=0;i<10;i++)
    {
        for(j=0;j<10;j++)
        {
            if(arr[i]<arr[j])
            {
                int_temp = arr[i];
                arr[i] = arr[j];
                arr[j] = int_temp;
            }
        }
    }
    ///Flag for checking the sorted list
    //for(i=1;i<3;i++)
    cout << "\nDisplaying the sorted array \n";
    for(i=1;i<10;i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;
    /// Flag for displaying the output
    cout << "\nDisplaying the names of the customers without sorting \n";

    for(i=0;i<10;i++)
    {
        cout << obj[i].get_name() << " ";
    }
    cout << endl;
    ///Displaying their names according to the sorted list

    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        fin.read((char *)& obj[i],sizeof(obj[i]));
        if(arr[i]==obj[i].get_check_in_date())
        {
            cout << obj[i].get_name() << " ";
        }
    }
    fin.close();

    /*
    fin.open("data.txt",ios::in);
    for(i=0;i<10;i++)
    {
        for(j=0;j<10;j++)
        {
                fin.read((char *)& obj[i],sizeof(obj[i]));
                    if(arr[i]==obj[j].get_check_in_date())
                    {
                        cout << obj[i].get_name() << " ";
                    }
        }
    }
    fin.close();
    */
}

void case9()
{
    fin.open("data.txt",ios::in);
    if("data.txt" == '\0')
    {
        cout << "No contents to show \n Please add the contents \n";
    }

    else
    {
        for(i=0;i<10;i++)
        {
            fin.read((char *)& obj[i],sizeof(obj[i]));
            obj[i].display();
        }
    }
    fin.close();
}
void case10()
{
    fout.open("data.txt",ios::app);
    for(i=0;i<10;i++)
    {
    obj[i].set();
    fout.write((char *)& obj[i],sizeof(obj[i]));
    }
    fout.close();

}
int main()
{
    int choice;
    char con;

cout << "\t\t\tHotel Management System \n";
cout << "1.Display all customers who have Delux room as type \n";
cout << "2.Display all customers who are checking out today \n";
cout << "3.Display all customers who want breakfast in their room \n";
cout << "4.Display all customers whose name start start with 'S' \n";
cout << "5.Display all the details of the customers whose location is 'Ahmedabad'\n";
cout << "6.Display all the customers who need guide and check in date is also today \n";
cout << "7.Display all customers according to room type \n";
cout << "8.Display all customers according to check in date latest to the earliest \n";
cout << "9.Display all the contents of the file \n";
cout << "10.Add the customers details \n";

again:
cout << "\t\t\t Enter your choice \n";
cin >> choice;

    switch(choice)
    {
        case 1:
            {
                case1();
                break;
            }
        case 2:
            {
                case2();
                break;
            }
        case 3:
            {
                case3();
                break;
            }
        case 4:
            {
                case4();
                break;
            }
        case 5:
            {
                case5();
                break;

            }
        case 6:
            {
                case6();
                break;
            }
        case 7:
            {
                case7();
                break;
            }
        case 8:
            {
                case8();
                break;
            }
        case 9:
            {
                case9();
                break;
            }
        case 10:
            {
                case10();
                break;
            }
        default:
            cout << "Invalid Input \n Try again \n";
            goto again;
    }
cout << "Want to continue.Yes 'y' or No 'n'\n";
cin >> con;
if(con=='y'||con=='Y')
{
    goto again;
}
else if(con=='n'||con=='N')
{
    cout << "Visit Again \n";
}

else
{
    cout << "Enter a valid input \n";
}


return 0;
}
