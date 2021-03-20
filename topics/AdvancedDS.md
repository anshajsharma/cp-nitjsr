<h1 align="center">
    CP Algorithms
 </h1>
 <h5 align="center">
   Author: Anshaj Kumar
 </h5>
 
 
 ### Contents  
 
| No. | Topics |
| --- | --------- |
|    | [*Special Notes*](#special-notes-) |
|    | **Advanced Data Structures** |
|1   | [Disjoint Set Data Structure](#disjoint-set-data-structure) |
|2   | [Segment Tree](#segment-tree)|
|    | [Lazy Propogation](#lazy-propogation) |
|3   | [Trie](#trie) |


##  Disjoint Set Data Structure

Consider a situation with a number of persons and following tasks to be performed on them.  

1.  Add a new friendship relation, i.e., a person x becomes friend of another person y.  
2.  Find whether individual x is a friend of individual y (direct or indirect friend)  

```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fr(i,j,n)    for(ll i=j;i<n;i++)
#define tc           ll t1; cin>>t1; while(t1--)
#define inp          ll n; cin>>n; ll a[n]; fr(i,0,n) cin>>a[i];
#define inp1         ll n1; cin>>n1; ll a[n1]; fr(i,0,n1) cin>>a[i];
#define vec          vector<ll>
#define pb           push_back
#define pii          pair<ll,ll>
#define mp           make_pair
#define F            first
#define S            second
#define fast         ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)      lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)      upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long           mod=pow(10,9)+7;

class DisjSet { 
    int *rank, *parent, n; 
  
public: 
    // Constructor to create and initialize sets of n items 
    DisjSet(int n) 
    { 
        rank = new int[n]; 
        parent = new int[n]; 
        this->n = n; 
        makeSet(); 
    } 
  
    // Creates n single item sets 
    void makeSet() 
    { 
        for (int i = 0; i < n; i++) { 
            parent[i] = i; 
        } 
    } 
  
    // Finds set of given item x 
    int find(int x) 
    { 
        // Finds the representative of the set that x is an element of 
        if (parent[x] != x) { 
  
            // if x is not the parent of itself Then x is not the representative of his set, 
            parent[x] = find(parent[x]);    // Known as path compression
  
        } 
  
        return parent[x]; 
    } 
  
    // Do union of two sets represented by x and y. 
    void Union(int x, int y) 
    { 
        // Find current sets of x and y 
        int xset = find(x); 
        int yset = find(y); 
  
        // If they are already in same set 
        if (xset == yset) 
            return; 
  
        // Put smaller ranked item under  bigger ranked item if ranks are different 
        if (rank[xset] < rank[yset]) { 
            parent[xset] = yset; 
        } 
        else if (rank[xset] > rank[yset]) { 
            parent[yset] = xset; 
        } 
  
        // If ranks are same, then increment 
        // rank. (Here xset or yset anyone can be treated as parent.)
        // In my case xset is treated as
        else { 
            parent[yset] = xset; 
            rank[xset] = rank[xset] + 1; 
        } 
    } 
}; 
void solve()
{
    DisjSet obj(5);  // creates disjoint set of size 5
    obj.Union(0, 2);         
    obj.Union(4, 2); 
    obj.Union(3, 1); 

              //     0
              //       \
              //   1     2
              //  /       \
              // 3         4

    // check if 4 and 0 belongs to same set or not (YES)
    if (obj.find(4) == obj.find(0)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 

    // check if 4 and 0 belongs to same set or not (NO)
    if (obj.find(1) == obj.find(0)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif
    
      solve();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}


```

**[⬆ Back to Top](#----cp-algorithms-)** 

## Segment Tree  

**Build:** *Both Time and Space Complexicity of build is **O(N)***
```c++
void build(int node, int start, int end)
{
    if(start == end)
    {
        tree[node] = A[start];
    }
    else
    {
        int mid = (start + end) / 2;
        build(2*node, start, mid);
        build(2*node+1, mid+1, end);
        // Internal node will have the sum of both of its children
        tree[node] = tree[2*node] + tree[2*node+1];
    }
}
```  
**Query:** *Time Complexicity of query is **O(logN)***  
```c++
int query(int node, int start, int end, int l, int r)
{
    if(r < start || end < l)  return 0;           //no overlap
    if(l <= start && end <= r) return tree[node]; //complete overlap
    
    // range represented by a node is partially inside and partially outside the given range
    int mid = (start + end) / 2;
    int p1 = query(2*node, start, mid, l, r);
    int p2 = query(2*node+1, mid+1, end, l, r);
    return (p1 + p2);
}
```  
**Update:** *Time Complexicity of update is **O(logN)***   
```c++
void update(int node, int start, int end, int idx, int val)
{
    if(start == end)
    {
        // Leaf node (here idx will be equal to start and end)
        A[idx] += val;
        tree[node] += val;
    }
    else
    {
        int mid = (start + end) / 2;
        if(start <= idx and idx <= mid) update(2*node, start, mid, idx, val);
        else                            update(2*node+1, mid+1, end, idx, val);

        // storing sum of both of its children
        tree[node] = tree[2*node] + tree[2*node+1];
    }
}
```  
## Lazy Propogation
**Now for range update we use lazy propogation**  
  
  
>  **Note:** In below code I used 0 based indexing of segment tree.(Diff. from upper one)  
  
**Build** (Same as above)   
  
```c++
const int N=200005;
ll seg[4*N];
void build(ll ind,ll l,ll r){  // build(0,0,n-1);
    if(l>r)
    return;
    if(l==r){
        seg[ind]=0;
        return;
    }
    ll mid=(l+r)/2;
    build(2*ind+1,l,mid);
    build(2*ind+2,mid+1,r);
 
    seg[ind]= seg[2*ind+1]+seg[2*ind+2];
}

```
**Lazy Propogation Update**  
```c++
ll lazy[4*N];
void update(ll ind,ll l,ll r,ll lq,ll rq, ll val){  //update(0,0,n-1,lq,rq,val);
    if(lazy[ind]!=0){
        seg[ind]=(r-l+1)*lazy[ind];
        if(l!=r){
            lazy[ind*2+1]=lazy[ind];
            lazy[ind*2+2]=lazy[ind];
        }
        lazy[ind]=0;
    }
    if(l>r||r<lq||rq<l)
    return;
    if(l>=lq&&r<=rq){
        seg[ind]=(r-l+1)*val;
        if(l!=r){
            lazy[ind*2+1]=val;
            lazy[ind*2+2]=val;
        }
        return;
    }
    ll mid=(l+r)/2;
    update(2*ind+1,l,mid,lq,rq,val);
    update(2*ind+2,mid+1,r,lq,rq,val);
 
    seg[ind]= seg[2*ind+1]+seg[2*ind+2];
}
 
```  
**Lazy Propogation Query**    
```c++
ll query(ll ind,ll l,ll r,ll lq,ll rq){  //query(0,0,n-1,lq,rq);   sum on interval [lq, rq]
    if(l>r||r<lq||rq<l)
        return 0;
    if(lazy[ind]!=0){
        seg[ind]=(r-l+1)*lazy[ind];
        if(l!=r){
            lazy[ind*2+1]=lazy[ind];
            lazy[ind*2+2]=lazy[ind];
        }
        lazy[ind]=0;
    }
 
    if(l>=lq&&r<=rq)
        return seg[ind];
 
    ll mid=(l+r)/2;
 
    ll k1,k2;
    k1=query(2*ind+1,l,mid,lq,rq);
    k2=query(2*ind+2,mid+1,r,lq,rq);
 
    return k1+k2;
}

```
**[⬆ Back to Top](#----cp-algorithms-)** 


## Trie  
**Initialising trie DS.**
```c++
struct trie{
  trie *a[26];
  bool isLastChar;

  trie(){
    isLastChar = false;
    for(int i=0;i<26;i++)
    a[i]=NULL;
  }
};
```  
**Insertion in trie.**
```c++
void insert(trie *root,int lev,string s)
{
    trie *p = root;
    int l= s.size();
    for (int i = 0; i < l; i++)
    {
        int index = s[i] - 'a';
        if (!p->a[index])
            p->a[index] = new trie();

        p = p->a[index];
    }
    p->isLastChar = true;
}
```  
**Searching in trie.**
```c++
bool search(trie *root,string s)
{
    int len=s.size();
    int lev=0;
    while(lev!=len)
    {
        int ind=s[lev]-'a';
        if(root->a[ind]==NULL) return false;
         root=root->a[ind];
        lev++;
    }
    return root->isLastChar;
}
```  
**Deletion in trie.**
```c++
void  deleteStr(trie * root,string s)
{
    int len=s.size();
    int lev=0;
    while(lev!=len)
    {
        int ind=s[lev]-'a';
        if(root->a[ind]==NULL) return ;
        root=root->a[ind];
        lev++;
    }
    root->isLastChar=false;
}
```
**Problems Link:**  
*  https://www.hackerearth.com/practice/data-structures/advanced-data-structures/trie-keyword-tree/practice-problems/algorithm/prasanjeet-verma-and-his-sorrow/  
*  https://www.hackerearth.com/practice/data-structures/advanced-data-structures/trie-keyword-tree/practice-problems/algorithm/search-engine/ (Good One)    
*  https://www.hackerearth.com/practice/data-structures/advanced-data-structures/trie-keyword-tree/practice-problems/algorithm/cost-of-data-11/  
  
  
    
```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fr(i,j,n)    for(ll i=j;i<n;i++)
#define tc           ll t1; cin>>t1; while(t1--)
#define inp          ll n; cin>>n; ll a[n]; fr(i,0,n) cin>>a[i];
#define inp1         ll n1; cin>>n1; ll a[n1]; fr(i,0,n1) cin>>a[i];
#define vec          vector<ll>
#define pb           push_back
#define pii          pair<ll,ll>
#define mp           make_pair
#define F            first
#define S            second
#define fast         ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)      lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)      upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_LONG_MAX
#define zer          LONG_MIN
const long           mod=pow(10,9)+7;

struct trie{
  trie *a[26];
  bool isLastChar;

  trie(){
    isLastChar = false;
    for(int i=0;i<26;i++)
    a[i]=NULL;
  }
};
void insert(trie *root,int lev,string s)
{
    trie *p = root;
    int l= s.size();
    for (int i = 0; i < l; i++)
    {
        int index = s[i] - 'a';
        if (!p->a[index])
            p->a[index] = new trie();

        p = p->a[index];
    }
    p->isLastChar = true;
}
bool search(trie *root,string s)
{
    int len=s.size();
    int lev=0;
    while(lev!=len)
    {
        int ind=s[lev]-'a';
        if(root->a[ind]==NULL) return false;
         root=root->a[ind];
        lev++;
    }
    return root->isLastChar;
}

int main()
{
  #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
  #endif

    trie *dictionary = new trie();
    insert(dictionary,0,"abc");
    insert(dictionary,0,"abcd");
    insert(dictionary,0,"abcssd");
    insert(dictionary,0,"adfbc");
    if(search(dictionary,"abcg")) cout<<"YES";
    if(!search(dictionary,"abcg")) cout<<"NO";
    cout<<endl;
    if(search(dictionary,"abc")) cout<<"YES";
    if(!search(dictionary,"abc")) cout<<"NO";
    cout<<endl;
    if(search(dictionary,"ab")) cout<<"YES";
    if(!search(dictionary,"ab")) cout<<"NO";

   return 0;
}

// Output:
// NO
// YES
// NO

```

**[⬆ Back to Top](#----cp-algorithms-)** 


