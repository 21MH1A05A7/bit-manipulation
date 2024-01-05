How  to calculate AND of ranged numbers in a array in O(1)
Using Prefix Matrix;

Idea: count set bits and see if the position has (l-r) number of set bits for the idea to happen without loops


in the prefix matrix every element have a value of set bit count from its previous element bit sum

PROGRAM:
=========
    // Online C++ compiler to run C++ program online
#include <bits/stdc++.h>
using namespace std;

int main() {
    // Write C++ code here
    // [7,1,5,2,3,9]
    //q1==>0,4
    //q2==>1,5
    //q3==>2,3
    int arr[6]={7,2,7,2,3,9};
    int mat[6][32];
    
    //PREFIX MATRIX;

    for(int i=0;i<6;i++){
        for(int j=31;j>=0;j--){
            if(i==0){
                if(arr[i]&(1<<j)){
                    mat[i][j]=1;    
                }
                else{
                    mat[i][j]=0;
                }
            }
            else{
                if(arr[i]&(1<<j)){
                    mat[i][j]=mat[i-1][j]+1;    
                }
                else{
                    mat[i][j]=mat[i-1][j];
                }
                
            }
        }
    }
    for(int i=0;i<6;i++){
        for(int j=10;j>=0;j--){
            cout<<mat[i][j]<<" ";
        }
        cout<<endl;
    }

    int l=0;
    int r=2;
    int total_ele=(r-l)+1;
    int len=log2(arr[r])+1;
    int s=0;
    for(int i=0;i<len;i++){
        if(l>0){ //IF L IS NOT 0 THEN SUBTRACT 
            mat[r][i]=mat[r][i]-mat[l-1][i];
        }
        if(mat[r][i]==total_ele){
            s=s+(pow(2,i));
        }
    }
    cout<<s;
    // cout<<s;
    return 0;
}


// PROGRAM FOR (OR)
PROGRAM
========

// Online C++ compiler to run C++ program online
#include <bits/stdc++.h>
using namespace std;


//OR
int main() {
    int arr[6]={7,2,7,2,3,9};
    int mat[6][32];
    
    for(int i=0;i<6;i++){
        for(int j=31;j>=0;j--){
            if(i==0){
                if((arr[i]&(1<<j))){
                    mat[i][j]=1;    
                }
                else{
                    mat[i][j]=0;
                }
            }
            else{
                if((arr[i]&(1<<j))){
                    mat[i][j]=mat[i-1][j]+1;    
                }
                else{
                    mat[i][j]=mat[i-1][j];
                }
                
            }
        }
    }
    for(int i=0;i<6;i++){
        for(int j=10;j>=0;j--){
            cout<<mat[i][j]<<" ";
        }
        cout<<endl;
    }

    int l=0;
    int r=2;
    int total_ele=(r-l)+1;
    int len=log2(arr[r])+1;
    int s=0;
    for(int i=0;i<len;i++){
        if(mat[l][i]>0){
            s+=(pow(2,i));
        }
    }
    cout<<s;
    // cout<<s;
    return 0;
}





