# -
初学者仓库
#include <iostream>
#include <string>
#define MAX 1000
using namespace std;
struct person
{
    string m_name;
    int m_sex;//1 man ,2 woman
    int m_age;
    string m_phone;
    string m_address;
};
struct addressbooks
{
    struct person array[MAX];
    int m_size;
};
void addperson(addressbooks * add1)
{
    if(add1->m_size == MAX)
    {
        cout << "the addressbook is full,you cannot add anything!"<<endl;
        return;
    }
    else 
    {
        string name;
        cout << "please add your name:"<< endl;
        cin >> name;
        add1->array[add1->m_size].m_name = name;
        //将你输入的名字存储到通讯录的通讯人数组的名字部分中，顺序号刚好为通讯录目前的人数
        
        int sex = 0;
        cout <<"please show your gender:"<< endl;
        cout <<"1---man"<< endl;
        cout <<"2---woman"<< endl;
        while(1)
        { 
            cin >> sex;
            if(sex == 1||sex == 2)
        {
            add1->array[add1->m_size].m_sex = sex;
            break; 
        }
        cout << "please show your true gender!  try again."<<endl;
        }

        cout << "please add your age :"<< endl;
        int age = 0;
        cin >> age;
        add1->array[add1->m_size].m_age = age;

        cout << "please add your phone :"<< endl;
        string phone;
        cin >> phone;
        add1->array[add1->m_size].m_phone = phone;
       
        cout << "please add your address :"<< endl;
        string address;
        cin >> address;
        add1->array[add1->m_size].m_address = address;

        add1->m_size++;
        cout << "successful add!"<< endl;
        system("pause");
        system("cls");
    }
}
void showperson(addressbooks * add1)
{
    if(add1->m_size == 0)
    {
        cout << "the addressbook is NULL!" <<endl;
    }
    else
    {
        for(int i = 0;i < add1->m_size; i++)
        {
            cout << "CONTACT----"<< i+1 << endl;
            cout << "name:  "<< add1->array[i].m_name<<"\t";
            cout << "sex:  "<< (add1->array[i].m_sex == 1 ? "man" : "woman")<<"\t";
            cout << "age:  "<< add1->array[i].m_age<<"\t";
            cout << "phone  :"<< add1->array[i].m_phone<<"\t";
            cout << "address:  "<< add1->array[i].m_address<<endl;
        }    
    }
    system("pause");
    system("cls");
}
int isexist(addressbooks * add1,string name)//检测联系人是否存在
//如果存在返回联系人所在数组中具体位置，不存在返回-1
//参数一  通讯录    参数二  对比姓名
{
    for(int i = 0;i < add1->m_size;i++)
    {
        if(add1->array[i].m_name == name)
        {
            return i;//找到了，返回数组下标编号
        }
    }
    return -1;//如果遍历结束都没找到，返回-1
}
void deleteperson(addressbooks * add1)
{
    cout << "show the contact's name that you want to delete: "<<endl;
    string name;
    cin >> name;
    int ret = isexist(add1,name);
    if(ret == -1)
    {
        cout << "there is none of this contact!"<< endl;
    }
    else
    {
        for(int i = ret;i < add1->m_size;i++)
        {
            add1->array[i] = add1->array[i+1];//让通讯录后一个人的信息覆盖前一个人，
            //实现ret号的信息删除和通讯录序号更新
        }
        add1->m_size--;//更新通讯录人员数
        cout << "delete sucessfully!" << endl;
    }
    system("pause");
    system("cls");
}
void findperson(addressbooks * add1)
{
    cout << "show the contact that you want to find:"<< endl;
    string name;
    cin >> name;
    int ret = isexist(add1,name);
    if (ret == -1)
    {
        cout << "there is none of this contact!"<< endl;
    }
    else
    {
        cout << "CONTACT----"<< ret + 1 << endl;
        cout << "name:  "<< add1->array[ret].m_name<<"\t";
        cout << "sex:  "<< (add1->array[ret].m_sex == 1 ? "man" : "woman")<<"\t";
        cout << "age:  "<< add1->array[ret].m_age<<"\t";
        cout << "phone  :"<< add1->array[ret].m_phone<<"\t";
        cout << "address:  "<< add1->array[ret].m_address<<endl;
    }
    system("pause");
    system("cls");
}
void modifyperson(addressbooks * add1)
{
    cout << "show the contact that you want to modify: "<< endl;
    string name1;
    cin >> name1;
    int ret = isexist(add1,name1);
    if(ret == -1)
    {
        cout << "there is none of this contact!"<< endl;
    }
    else
    {
        string name;
        cout << "please add name you want to exchange:"<< endl;
        cin >> name;
        add1->array[ret].m_name = name;
        int sex = 0;
        cout <<"please show your gender:"<< endl;
        cout <<"1---man"<< endl;
        cout <<"2---woman"<< endl;
        while(1)
        { 
            cin >> sex;
            if(sex == 1||sex == 2)
        {
            add1->array[ret].m_sex = sex;
            break; 
        }
        cout << "please show your true gender!  try again."<<endl;
        }

        cout << "please add your age :"<< endl;
        int age = 0;
        cin >> age;
        add1->array[ret].m_age = age;

        cout << "please add your phone :"<< endl;
        string phone;
        cin >> phone;
        add1->array[ret].m_phone = phone;
       
        cout << "please add your address :"<< endl;
        string address;
        cin >> address;
        add1->array[ret].m_address = address;
        cout << "exchange sucessfully!"<<endl;
    }
   
    system("pause");
    system("cls");
}
void cleanperson(addressbooks * add1)
{
    add1->m_size = 0;//将当前记录联系人数量记为0
    cout << "the address has been cleaned!"<< endl;
    system("pause");
    system("cls");
}
void showmenu()//创建菜单
{
    cout << "***************************" << endl;
    cout << "***** 1,add contact *******" << endl;
    cout << "***** 2,show contact ******" << endl;
    cout << "**** 3,delete contact *****" << endl;
    cout << "***** 4,find contact ******" << endl;
    cout << "**** 5,exhange contact ****" << endl;
    cout << "***** 6,clean contact *****" << endl;
    cout << "********* 0,exit **********" << endl;
    cout << "***************************" << endl;
}
int main()
{
    addressbooks add1;
    add1.m_size = 0;
    int select = 0;
    while(1)
{
    showmenu();
MENU:
    cin >> select;//输入用户数字变量
    switch (select)
    {
    case 1: //1,add contact
    addperson(&add1);//利用地址传递，添加通讯人
        break;
    case 2://2,show contact
    showperson(&add1);
        break;
    case 3://3,delete contact
    deleteperson(&add1);
        break;
    case 4: //4,find contact
    findperson(&add1);
        break;
    case 5: //5,exhange contact
    modifyperson(&add1);
        break;
    case 6: //6,clean contact
    cleanperson(&add1);
        break;
    case 0://0,exit
        cout << "looking forward to your next usage." << endl;
        system("pause");
        return 0;
        break;
    default://输入错误
    cout << "please use legal number " << "(0~6)" <<endl;
    goto MENU;
        break;
    }
}
    //system("pause");
    return 0;
}
