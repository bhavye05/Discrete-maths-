# Discrete-Maths-Practicals

#### Ques1:1. Create a class SET. Create member functions to perform the following SET operations: a. is member: check whether an element belongs to the set or not and return value as true/false. b. powerset: list all the elements of the power set of a set. c. subset: check whether one set is a subset of the other or not. d. union and intersection of two Sets. e. complement: assume universal set as per the input elements from the user. f. set difference and symmetric difference between two sets. g. cartesian product of sets. Write a menu driven program to perform the above functions on an instance of the SET class.
```
#include <iostream>
#include <vector>
using namespace std;

class SET {
public:
    vector<int> s;

    void input() {
        int n, x;
        cout<<"Enter number of elements: ";
        cin>>n;
        cout<<"Enter elements:\n";
        for(int i=0;i<n;i++){
            cin>>x;
            s.push_back(x);
        }
    }

    bool isMember(int x){
        for(int i=0;i<s.size();i++){
            if(s[i]==x) return true;
        }
        return false;
    }

    void powerSet(){
        int n = s.size();
        int pow = 1<<n;

        for(int i=0;i<pow;i++){
            cout<<"{ ";
            for(int j=0;j<n;j++){
                if(i & (1<<j))
                cout<<s[j]<<" ";
            }
            cout<<"}\n";
        }
    }

    bool subset(SET b){
        for(int i=0;i<s.size();i++){
            if(!b.isMember(s[i]))
            return false;
        }
        return true;
    }

    void unionSet(SET b){
        cout<<"Union: ";
        for(int i=0;i<s.size();i++)
        cout<<s[i]<<" ";

        for(int i=0;i<b.s.size();i++){
            if(!isMember(b.s[i]))
            cout<<b.s[i]<<" ";
        }
        cout<<endl;
    }

    void intersection(SET b){
        cout<<"Intersection: ";
        for(int i=0;i<s.size();i++){
            if(b.isMember(s[i]))
            cout<<s[i]<<" ";
        }
        cout<<endl;
    }

    void difference(SET b){
        cout<<"Difference: ";
        for(int i=0;i<s.size();i++){
            if(!b.isMember(s[i]))
            cout<<s[i]<<" ";
        }
        cout<<endl;
    }

    void symmetricDifference(SET b){
        cout<<"Symmetric Difference: ";

        for(int i=0;i<s.size();i++){
            if(!b.isMember(s[i]))
            cout<<s[i]<<" ";
        }

        for(int i=0;i<b.s.size();i++){
            if(!isMember(b.s[i]))
            cout<<b.s[i]<<" ";
        }
        cout<<endl;
    }

    void cartesianProduct(SET b){
        cout<<"Cartesian Product:\n";
        for(int i=0;i<s.size();i++){
            for(int j=0;j<b.s.size();j++){
                cout<<"("<<s[i]<<","<<b.s[j]<<") ";
            }
        }
        cout<<endl;
    }
};

int main(){

    SET A,B;
    int choice,x;

    cout<<"Enter Set A\n";
    A.input();

    cout<<"Enter Set B\n";
    B.input();

    do{
        cout<<"\n1. Is Member\n2. Power Set\n3. Subset\n4. Union\n5. Intersection\n6. Difference\n7. Symmetric Difference\n8. Cartesian Product\n9. Exit\n";

        cin>>choice;

        switch(choice){

            case 1:
            cout<<"Enter element:";
            cin>>x;
            if(A.isMember(x))
            cout<<"True\n";
            else
            cout<<"False\n";
            break;

            case 2:
            A.powerSet();
            break;

            case 3:
            if(A.subset(B))
            cout<<"A is subset of B\n";
            else
            cout<<"Not a subset\n";
            break;

            case 4:
            A.unionSet(B);
            break;

            case 5:
            A.intersection(B);
            break;

            case 6:
            A.difference(B);
            break;

            case 7:
            A.symmetricDifference(B);
            break;

            case 8:
            A.cartesianProduct(B);
            break;

        }

    }while(choice!=9);

}
```

<img width="610" height="566" alt="image" src="https://github.com/user-attachments/assets/860b7514-d29d-410d-b679-f126c8729077" />
<img width="730" height="728" alt="image" src="https://github.com/user-attachments/assets/d4a0d20a-b2cf-40ca-964d-cb2fbbcc5f83" />

#### Ques2.Create a class RELATION, use Matrix notation to represent a relation. Include member functions to check if the relation is Reflexive, Symmetric, Anti-symmetric, Transitive. Using these functions check whether the given relation is: Equivalence or Partial Order relation or None

```
#include<iostream>
using namespace std;

class RELATION{

int a[10][10],n;

public:

void input(){
cout<<"Enter number of elements:";
cin>>n;

cout<<"Enter relation matrix:\n";
for(int i=0;i<n;i++){
for(int j=0;j<n;j++){
cin>>a[i][j];
}
}
}

bool reflexive(){
for(int i=0;i<n;i++)
if(a[i][i]!=1)
return false;
return true;
}

bool symmetric(){
for(int i=0;i<n;i++)
for(int j=0;j<n;j++)
if(a[i][j]!=a[j][i])
return false;
return true;
}

bool antisymmetric(){
for(int i=0;i<n;i++)
for(int j=0;j<n;j++)
if(i!=j && a[i][j]==1 && a[j][i]==1)
return false;
return true;
}

bool transitive(){
for(int i=0;i<n;i++)
for(int j=0;j<n;j++)
for(int k=0;k<n;k++)
if(a[i][j] && a[j][k] && !a[i][k])
return false;

return true;
}

void checkRelation(){

bool r = reflexive();
bool s = symmetric();
bool a = antisymmetric();
bool t = transitive();

if(r && s && t)
cout<<"Equivalence Relation\n";

else if(r && a && t)
cout<<"Partial Order Relation\n";

else
cout<<"None\n";
}

};

int main(){

RELATION R;

R.input();

R.checkRelation();

}
```
<img width="620" height="217" alt="image" src="https://github.com/user-attachments/assets/1f282f6d-92fa-42dd-ac63-d1c2fa9b6a78" />

#### Ques3. 3. Write a Program that generates all the permutations of a given set of digits, with or without repetition.
```
#include<iostream>
using namespace std;

void permute(string s,int l,int r){

if(l==r)
cout<<s<<endl;

else{

for(int i=l;i<=r;i++){

swap(s[l],s[i]);

permute(s,l+1,r);

swap(s[l],s[i]);

}
}
}

int main(){

string s;

cout<<"Enter digits:";
cin>>s;

permute(s,0,s.length()-1);

}
```
<img width="571" height="711" alt="image" src="https://github.com/user-attachments/assets/4e93fb61-141a-4b0e-b8cf-1edb542697ba" />


#### Ques4.For any number n, write a program to list all the solutions of the equation x1 + X2 + X3 + ... + Xn = C, where C is a constant (C <= 10) and X1, X2, X3, ... ,Xn are nonnegative integers, using brute force strategy.

```
#include<iostream>
using namespace std;

int n,C;
int x[10];

void solve(int k,int sum){

if(k==n){

if(sum==C){
for(int i=0;i<n;i++)
cout<<x[i]<<" ";
cout<<endl;
}

return;
}

for(int i=0;i<=C;i++){

x[k]=i;

if(sum+i<=C)

solve(k+1,sum+i);

}
}

int main(){

cout<<"Enter n:";
cin>>n;

cout<<"Enter C:";
cin>>C;

solve(0,0);

}
```
<img width="585" height="651" alt="image" src="https://github.com/user-attachments/assets/2eeb6976-4229-48d3-895a-be02a71c57e5" />


#### Ques5. Write a Program to evaluate a polynomial function. (For example store f(x) = 4n2 + 2n + 9 in an array and for a given value of n, say n = 5, compute the value of f(n)).

```
#include<iostream>
using namespace std;

int main(){

int coef[3]={4,2,9};
int n;

cout<<"Enter value of n:";
cin>>n;

int result = coef[0]*n*n + coef[1]*n + coef[2];

cout<<"Result = "<<result;

}
````

<img width="514" height="148" alt="image" src="https://github.com/user-attachments/assets/929d009f-7f03-4049-8d92-656171aacae1" />


#### Ques6. Write a Program to check if a given graph is a complete graph. Represent the graph using the Adjacency Matrix representation.

```
#include<iostream>
using namespace std;

int main(){

int n,a[10][10],flag=1;

cout<<"Enter number of vertices:";
cin>>n;

cout<<"Enter adjacency matrix:\n";

for(int i=0;i<n;i++){
for(int j=0;j<n;j++){
cin>>a[i][j];
}
}

for(int i=0;i<n;i++){
for(int j=0;j<n;j++){

if(i!=j && a[i][j]==0)
flag=0;

}
}

if(flag==1)
cout<<"Complete Graph";

else
cout<<"Not Complete Graph";

}
```
<img width="440" height="220" alt="image" src="https://github.com/user-attachments/assets/d1fba919-e143-440b-960b-07dbc400729c" />

#### Ques7. Write a Program to accept a directed graph G and compute the in-degree and outdegree of each vertex.
```
#include<iostream>
using namespace std;

int main(){

int n,a[10][10];

cout<<"Enter number of vertices:";
cin>>n;

cout<<"Enter adjacency matrix:\n";

for(int i=0;i<n;i++){
for(int j=0;j<n;j++){
cin>>a[i][j];
}
}

for(int i=0;i<n;i++){

int indeg=0,outdeg=0;

for(int j=0;j<n;j++){

outdeg += a[i][j];
indeg += a[j][i];

}

cout<<"Vertex "<<i+1<<" In-degree = "<<indeg<<" Out-degree = "<<outdeg<<endl;

}

}
```











<img width="492" height="272" alt="image" src="https://github.com/user-attachments/assets/9135ad22-e540-42f1-ba2a-a64f462b8c14" />






