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
|    | **Graph Related Topics** |
|1   | [Dijkstra's SSSP Algorithm](#dijkstras-sssp-algorithm) |
|2   | [Topological Sort](#topological-sort) |
|3   | [Disjoint Set Data Structure](#disjoint-set-data-structure) |
|4   | [Kruskal's Algorithm MST](#kruskals-algorithm-mst) |
|5   | [Cycle Detection Using DS](#cycle-detection-using-ds) |
|6   | [Strongly Connected Components](#strongly-connected-components) |
|7   | [Prim's Algorithm MST](#prims-algorithm-mst) |
|8   | [Circumference of Tree](#circumference-of-tree) |
|9   | [Cycle Detection In Directed Graph](#cycle-detection-in-directed-graph) |
|10  | [Lowest Common Ancestor-Binary Lifting](#lowest-common-ancestor-binary-lifting) |
|11  | [Articulation Point](#articulation-point) |

##  Dijkstra's SSSP Algorithm

You are given a directed or undirected weighted graph with n vertices and m edges. The weights of all edges are non-negative. You are also given a starting vertex s. This article discusses finding the lengths of the shortest paths from a starting vertex s to all other vertices, and output the shortest paths themselves.  
  
This problem is also called **single-source shortest paths problem.**

*  **Dijkstra's algorthm fails in case of graph containing negative cycle or negative edge weight.**   

>  https://codeforces.com/contest/20/problem/C  

```C++
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

vector<pair<ll , ll> > adj[100001];
int visited[100001]={0};
ll parent[100001]={-1};
ll dis[100001];
map<pair<ll , ll> , ll> m;
void fillup() 
{
 for(int i=0;i<100001;i++)
  {parent[i]=-1; visited[i]=0; dis[i]=inf;}
}
void addWeitageEdge(ll a,ll b,ll c)
{
    //if(m(mp<a,b>)) 
           adj[a].pb(mp(b,c));
  if(a!=b) adj[b].pb(mp(a,c));  //if undirected
}

// Time Complexicity: O(NlogE)
void dijkstra(ll s,ll n) {
    fillup();
   parent[s]=s;
 
    dis[s] = 0;
    set<pair<ll, ll>> q;
    q.insert({0, s});
    while (!q.empty()) {
        ll v = q.begin()->second;
        q.erase(q.begin());
 
        for (auto edge : adj[v]) {
            ll to = edge.F;
            ll len = edge.S;
 
            if (dis[v] + len < dis[to]) {
                //erase old pair
                q.erase({dis[to], to});
                dis[to] = dis[v] + len;
                parent[to] = v;
                //insert new one with less distance
                q.insert({dis[to], to});
            }
        }
    }
}
 
void printPath(ll st,ll dest,ll n)
{
  vector<ll> v;
  ll temp=dest;
  dijkstra(st,n);
  v.pb(dest);
  if(parent[st]!=-1 && parent[dest]!=-1)
  {
    while(parent[temp]!=st)
    {
      v.pb(parent[temp]);
      temp=parent[temp];
    }
    if(dest!=st) v.pb(st);
    ll n=v.size();
    while(n--)
    {
      cout<<v[n]<<" ";
    }
    cout<<endl;
  }
  else cout<<"-1"<<endl;
}
int main()
{
  #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
  #endif

   ll n,e;
    cin>>n>>e;
    ll a,b,c;
    for(int i=0;i<e;i++)
    {
      cin>>a>>b>>c;
      addWeitageEdge(a,b,c);
    }

   printPath(1,n,n);
   return 0;
}

// input         Output
// 5 6           1 4 3 5
// 1 2 2
// 2 5 5
// 2 3 4
// 1 4 1
// 4 3 3
// 3 5 1

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  Topological Sort

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

vector<int> ans;
std::vector<ll> v[maxx];
int visited[maxx];

void dfs(int root){
  visited[root]=1;
  for (int i:v[root])
  {
    if(!visited[i]) dfs(i);
  }
  ans.pb(root);
}
// Time Complexicity: O(n+e)
void topological_sort()
{
    int n,e;
    cin>>n>>e;
    fr(i,0,e){
      int x,y;
      cin>>x>>y;
      v[x].pb(y);    
    }

    for (int i = 0; i < n; ++i) {
        if (!visited[i])
            dfs(i);
    }
    reverse(ans.begin(), ans.end());
    int l=ans.size();
    fr(i,0,l) cout<<ans[i]<<" ";
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

     topological_sort();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Input           Output
// 3 2             2 0 1
// 0 1             
// 2 1             

// 5 5             0 2 1 3 4 
// 0 3
// 3 4
// 1 0
// 2 1
// 0 2
 

```

**[⬆ Back to Top](#----cp-algorithms-)** 



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


##  Kruskal's Algorithm MST
<h5 align="center">
   Image Src: HackerEarth
 </h5>   
 
![](https://github.com/anshajsharma/CP-Algorithms/blob/master/Data/6322896.jpg)  
 
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
    DisjSet(int n) 
    { 
        rank = new int[n]; 
        parent = new int[n]; 
        this->n = n; 
        makeSet(); 
    } 
    void makeSet() 
    { 
        for (int i = 0; i < n; i++) { 
            parent[i] = i; 
            rank[i]=0;
        } 
    } 
    int find(int x) 
    { 
        if (parent[x] != x) { 
            parent[x] = find(parent[x]);    // Known as path compression
        } 
        return parent[x]; 
    } 
    void Union(int x, int y) 
    { 
        int xset = find(x); 
        int yset = find(y); 
  
        // If they are already in same set 
        if (xset == yset) 
            return; 
  
        if (rank[xset] < rank[yset]) { 
            parent[xset] = yset; 
        } 
        else if (rank[xset] > rank[yset]) { 
            parent[yset] = xset; 
        } 
        else { 
            parent[yset] = xset; 
            rank[xset] = rank[xset] + 1; 
        } 
    } 
}; 

struct edge
{
  ll x,y,weight;
};

bool comp(edge a,edge b)
{
  return a.weight<b.weight;
}

//Time Complexicity: O(NlogE) or O(ElogN)
void kruskalAlgoMST()
{
    ll n,e;
    cin>>n>>e;
    edge edges[e];

    fr(i,0,e) cin>>edges[i].x>>edges[i].y>>edges[i].weight;

    sort(edges,edges+e,comp);

    std::vector<edge> v;

    // DisjSet ds(n+1);  // for 1 based indexing
    DisjSet ds(n);      // for 0 based indexing

    fr(i,0,e){
      int parentX = ds.find(edges[i].x);
      int parentY = ds.find(edges[i].y);
      if(parentX==parentY) ;
      else {
        ds.Union(edges[i].x,edges[i].y);
        v.pb(edges[i]);
      }
    }
    int l = v.size();
    fr(i,0,l) cout<<v[i].x<<" "<<v[i].y<<" "<<v[i].weight<<endl;

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

      kruskalAlgoMST();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}

// input                 Output
// 5 7                    0 1 1
// 0 1 1                  3 4 2
// 0 2 7                  1 4 3
// 1 2 5                  1 2 5
// 1 3 4
// 1 4 3
// 3 4 2
// 2 4 6

```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Cycle Detection Using DS
**Concept Used:** For each edge, make subsets using both the vertices of the edge. If both the vertices are in the same subset, a cycle is found.  
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
    DisjSet(int n) 
    { 
        rank = new int[n]; 
        parent = new int[n]; 
        this->n = n; 
        makeSet(); 
    } 
    void makeSet() 
    { 
        for (int i = 0; i < n; i++) { 
            parent[i] = i; 
            rank[i]=0;
        } 
    } 
    int find(int x) 
    { 
        if (parent[x] != x) { 
            parent[x] = find(parent[x]);    // Known as path compression
        } 
        return parent[x]; 
    } 
    void Union(int x, int y) 
    { 
        int xset = find(x); 
        int yset = find(y); 
  
        // If they are already in same set 
        if (xset == yset) 
            return; 
  
        if (rank[xset] < rank[yset]) { 
            parent[xset] = yset; 
        } 
        else if (rank[xset] > rank[yset]) { 
            parent[yset] = xset; 
        } 
        else { 
            parent[yset] = xset; 
            rank[xset] = rank[xset] + 1; 
        } 
    } 
}; 

// Time Complexicity: O(n)
void solve()
{
    ll n,e;
    cin>>n>>e;
    DisjSet graph(n);  // creates disjoint set of size 5
    int f=0;
    fr(i,0,e){
        ll x,y;
        cin>>x>>y;
        if (graph.find(x) == graph.find(y)) f=1;
        graph.Union(x,y);
    }

    if (f) 
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

// input                 Output
// 5 7                    
// 0 1 1                  Yes
// 0 2 7                  
// 1 2 5                  
// 1 3 4
// 1 4 3
// 3 4 2
// 2 4 6

// 5 3                    No
// 0 2
// 2 4
// 4 1

```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Strongly Connected Components
A directed graph is strongly connected if there is a path between all pairs of vertices. A strongly connected component (SCC) of a directed graph is a maximal strongly connected subgraph. For example, there are 3 SCCs in the following graph.  
<h5 align="center">
   Image Src: GFG
 </h5>   
 
![](https://github.com/anshajsharma/CP-Algorithms/blob/master/Data/SCC.png)  
>  Given Algo named as **Kosaraju's Algorithm**   
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

//--------------------------------------------------
//Used for main graph
stack<int> s;
std::vector<ll> v[maxx];
int visited[maxx];

void dfs(int root){
  visited[root]=1;
  for (int i:v[root])
  {
    if(!visited[i]) dfs(i);
  }
  s.push(root);
}
//--------------------------------------------------
//Used for reversed graph
std::vector<ll> rv[maxx];
int rvisited[maxx]; 
std::vector<int> SCC[maxx];
int SccCount=0;
void rdfs(int root){
  rvisited[root]=1;

  SCC[SccCount].pb(root);

  for (int i:rv[root])
  {
    if(!rvisited[i]) rdfs(i);
  }

}
//--------------------------------------------------
void PrintStack(stack<int> s) 
{ 
    if (s.empty())  
        return; 
    int x = s.top(); 
    s.pop(); 
    PrintStack(s); 
    cout << x << " "; 
    s.push(x); 
} 
//--------------------------------------------------
// Time Complexicity: O(n+e)
void stronglyConnectedComponent()
{
    int n,e;
    cin>>n>>e;
    int st=-1;
    fr(i,0,e){
      int x,y;
      cin>>x>>y;
      if(st==-1) st=x;
      v[x].pb(y);    // Contains vertex
      rv[y].pb(x);   // Contains reverse vertex used for reverse graph
    }
    fr(i,0,n) // for 0 based indexing
    if(!visited[i]) dfs(i); 
    // PrintStack(s); cout<<endl;

    while(!s.empty()){
      int temp=s.top();
      s.pop();
      if(!rvisited[temp]) {
        rdfs(temp); SccCount++;
      }
    }
    cout<<"SCC Count: "<<SccCount<<endl;
    fr(i,0,SccCount){
      int l=SCC[i].size();
      fr(j,0,l){
        cout<<SCC[i][j]<<" ";
      }
      cout<<endl;
    }
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

     stronglyConnectedComponent();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Input           Output
// 3 2             SCC Count: 3
// 0 1             0
// 1 2             1
//                 2

// 11 13           SCC Count: 4
// 2 0             6 9 8 7 
// 0 1             10 
// 1 2             0 2 1 
// 1 3             3 5 4 
// 3 4
// 4 5
// 5 3
// 6 5
// 6 7
// 7 8
// 8 9
// 9 6
// 9 10

// 5 5             SCC Count: 3  (see above figure)      
// 0 3             0 1 2 
// 3 4             3
// 1 0             4
// 2 1
// 0 2

```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Prim's Algorithm MST

```c++

```

**[⬆ Back to Top](#----cp-algorithms-)** 



##  Circumference of Tree
*  **Concept used:** Pick any random node(*say a*) and find node(*say b*) having largest distance from it. Now again find final node(*say ans*) which is farthest from found node(*i.e. from b*)  
*  For *Tree* as only BFS is used 2 times Time complexicity: **O(V+E)** i.e. **O(N)**  
*  **NOTE:** For *Graph*, using this concept time complexicity will be **O(N^3)** (Think How??)  
>  https://www.youtube.com/watch?v=MOy4UDjN8DM (Tutorial)  
>  https://codeforces.com/gym/102694/problem/A  
>  https://codeforces.com/gym/102694/problem/B (Good One)
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
 
vector<ll> adj[500005];
int visited[500005]={0};
ll level[500005];
map<pair<ll , ll> , ll> m;
void fillup() 
{
 for(int i=0;i<500005;i++)
  { visited[i]=0; level[i]=-1; }
}
void addEdge(ll a,ll b)
{
           adj[a].pb(b);
  if(a!=b) adj[b].pb(a);  //if undirected
}
 
void bfs(int root)
{
  fillup();
  visited[root]=1;
  level[root]=0;
  queue<int> q;
  q.push(root);
  while(!q.empty()){
    ll t = q.front();
    q.pop();
    for( auto i : adj[t] )
    {
      if(!visited[i]){
        level[i] = level[t]+1;
        q.push(i);
        visited[i]=1;
      }
    }
 
  }
}
 
int main()
{
  #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
  #endif
 
   ll n;
   cin>>n;
   if(n==1){
    cout<<0; return 0;
   }
    fr(i,0,n){
      ll a,b;
      cin>>a>>b;
      addEdge(a,b);
    }
 
    bfs(1);
    int lstNode = -1,mx=-1;
    fr(i,1,n+1){
      if(level[i]>mx){
        mx=level[i]; lstNode=i;
      }
    }
    bfs(lstNode);
    lstNode = -1,mx=-1;
    fr(i,1,n+1){
      if(level[i]>mx){
        mx=level[i]; lstNode=i;
      }
    }
    // Here mx is diameter of tree.
    cout<<3*mx<<" ";
 
    
 
   return 0;
}
```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Cycle Detection In Directed Graph
*  **Concept Used:** Maintain three sets: 
    *  whiteSet for unvisited nodes
    *  greySet for nodes currently in use
    *  blackSet for nodes fully explored
    *  now, if we found the new nodes which we want to visit is alredy in greySet i.e. Cycle Exist.  
>  **Related Problems Link:**
*  https://leetcode.com/problems/course-schedule/
*  https://leetcode.com/problems/course-schedule-ii/  
*  https://leetcode.com/problems/course-schedule-iii/ (unsolved)

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

 
vector<ll> adj[500005];

void addDirectedEdge(ll a,ll b)
{
      adj[a].pb(b);
}
void moveElement(int num,set<int>& a,set<int>& b )
{
  a.erase(num); b.insert(num);
}
bool dfs(set<int> &whiteSet,set<int> &greySet,set<int> &blackSet,int root)
{
    moveElement(root,whiteSet,greySet);
    for(auto i : adj[root])
    {
      if(blackSet.find(i)!=blackSet.end())
      {
        continue;
      }
      else if(greySet.find(i)!=greySet.end())
      {
        return true;
      }else if(dfs(whiteSet,greySet,blackSet,i)){
        return true;
      }
    }
    moveElement(root,greySet,blackSet);
    return false;
}



void cycleDetectionInDirectedGraph()
{
  set<int> whiteSet;  // Contains Unvisited vertices
  set<int> greySet;   // Contains in use vertices
  set<int> blackSet;  // Contains explored vertices
  ll n,e;
  cin>>n>>e;
  ll a,b;
  fr(i,0,e){
    cin>>a>>b;
    addDirectedEdge(a,b);
  }
  fr(i,0,n){  // for 0 based indexing
    whiteSet.insert(i);
  }
  int f=0;
  while(whiteSet.size()>0){
    int root  = *whiteSet.begin();
    if(dfs(whiteSet,greySet,blackSet,root)) f=1;
  }
    
  if(f) cout<<"Yes"<<endl;
    else cout<<"No"<<endl;
}

int main()
{
  #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
  #endif

   cycleDetectionInDirectedGraph();

   return 0;
}


```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Lowest Common Ancestor-Binary Lifting

```c++
int tim=1,tin[100005],tout[100005];
int up[100005][20];

void dfs(int u,int pa)      // dfs(0,-1)
{
    level[u]=level[pa]+1;   // level child = level parent + 1
    tin[u]=++tim;           // In time
    par[u][0]=pa;           // immediate parent of u is pa 
    fr(i,1,20)               // As all ancestors of ancestors of current nodes is already explored using those we will update curr
        par[u][i]=par[par[u][i-1]][i-1];
    for(int v:g[u])
    {
        if(v!=pa)
            dfs(v,u);
    }
    tout[u]=++tim;
}

bool isansc(int u,int v)
{
    // u is parent of v if and only if it came before and left after v. 
    return ((tin[u]<=tin[v])&&(tout[u]>=tout[v]));   // equal when u==v
}

int lca(int u,int v)
{
    if(isansc(u,v))
        return u;
    if(isansc(v,u))
        return v;
    for(int i=19;i>=0;i--)
    {
        if(!isansc(par[u][i],v))   //Here we will find first node just below actual LCA which is not ancestor of both u and v.
            u=par[u][i];
    }
    return par[u][0];
}
```

**[⬆ Back to Top](#----cp-algorithms-)** 


##  Articulation Point
**Definition:** In a graph, a vertex is called an articulation point if removing it and all the edges associated with it results in the increase of the number of connected components in the graph.  

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

 
vector<ll> adj[500005];
ll timeC=1;
std::vector<int> parent(500005);
int visitedTime[500005];
int lowTime[500005];
void addEdge(ll a,ll b)
{
            adj[a].pb(b);
   if(a!=b) adj[b].pb(a);   
}
std::vector<int> articulationPts;
void dfs(int root,int p)
{
    parent[root]=p;
    visitedTime[root]=timeC;
    lowTime[root] = timeC;
    int childC = 0;
    timeC++;
    bool isAP = false;
    for(auto i:adj[root])
    {
      if(i==parent[root]) continue;
      if(!visitedTime[i]){
        // parent[i]=root;
        childC++;
        dfs(i,root);
        if( visitedTime[root] <= lowTime[i]){
          isAP = true;
        }else{
          lowTime[root] = min(lowTime[root],lowTime[i]); 
        }
      } else {
        lowTime[root] = min(lowTime[root],lowTime[i]); 
      }
    }

    if((parent[root]==-1 && childC>=2) || (parent[root]!=-1 && isAP))
    {
      // cout<<root<<" "<<childC<<" "<<parent[root]<<" "<<isAP<<endl;
      articulationPts.pb(root);
    }

}



void articulationPoints()
{
  ll n,e;
  cin>>n>>e;
  ll a,b;
  fr(i,0,e){
    cin>>a>>b;
    addEdge(a,b);
  }
  dfs(0,-1);
  int l=articulationPts.size();
  cout<<l<<endl;
  // fr(i,0,n) cout<<parent[i]<<" "<<lowTime[i]<<" "<<visitedTime[i]<<endl;
  fr(i,0,l) cout<<articulationPts[i]<<" ";
}

int main()
{
  #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
  #endif

   articulationPoints();

   return 0;
}
// Input    Output
// 5 5      2
// 0 1      3 2
// 0 2
// 1 2
// 2 3
// 3 4
```

**[⬆ Back to Top](#----cp-algorithms-)** 

