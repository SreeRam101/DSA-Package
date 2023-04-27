#include<iostream>
#include<stdlib.h>
#include<cstring>
using namespace std;


const int HASH_SIZE=11;
const int EMPTY_SLOT=-1;
int hash_table[HASH_SIZE];



void display()
{
    cout<<"ELEMENTS :"<<endl;
    for(size_t i=0;i<HASH_SIZE;i++)
    {
        if(hash_table[i]!=EMPTY_SLOT)
        {
            cout<<hash_table[i]<<endl;
            //cout<<"index: "<<i<<endl;
        }
    }
    cout<<"\n";
}


int main()
{
    // Initialize the hash table to -1

    memset(hash_table, -1, sizeof(hash_table));

    int data,opt,ind;
    while(1)
    {
        cout<<"Enter the option:\n1.Insert the element\n2.Search for the element\n3.Delete the element\n4.Display the HASH table\n5.Exit\n ";
        cin>>opt;

        switch(opt)
        {
            case(1):
                cout<<"Enter the data: ";
                cin>>data;
                //hash function
                ind= data%HASH_SIZE;
                if(hash_table[ind]==EMPTY_SLOT)
                {
                    hash_table[ind]=data;
                }
                else // else part to handle collision using quadratic probing
                {
                    int flag=0;
                    int i=0;
                    while(i<HASH_SIZE)
                    {
                        ind=(data+(i*i))%HASH_SIZE;
                        if(hash_table[ind] == EMPTY_SLOT)
                        {
                            flag=1;
                            hash_table[ind]=data;
                            break;
                        }
                        if(flag==0 && (i==HASH_SIZE-1))
                            cout<<"NO FREE SLOT!\n";
                        i++;

                    }
                }
                break;
            case 2:
                int search;
                cout<<"Enter the element to be searched:";
                cin>>search;
                ind=search%HASH_SIZE;
                if(hash_table[ind]==search)
                {
                    cout<<"Element found"<<endl;
                }
                else
                {
                    int flag=0;
                    int i=0;
                    while(i<HASH_SIZE)
                    {
                        ind=(search+(i*i))%HASH_SIZE;
                        if(hash_table[ind]==search)
                        {
                            flag=1;
                            cout<<"Element found"<<endl;
                            break;
                        }
                        i++;
                        if(flag==0&&(i==HASH_SIZE-1))
                        {
                            cout<<"Element not found"<<endl;
                            break;
                        }
                    }
                }
                break;

            case 3:



                break;

            case(4):
               display();
               break;
            case 5:
                return 0;
            default:
                cout<<"Enter the options from 1 to 5"<<endl;
                break;
        }
    }
}
