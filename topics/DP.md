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
|    | **Dyamic Programming** |
|1   | [Matrix Chain Multiplication](#matrix-chain-multiplication) |
|2   | [Longest Palindromic Subsequence](#longest-palindromic-subsequence) |
|3   | [Longest Common Subsequence](#longest-common-subsequence) |
|4   | [Longest Common Substring](#longest-common-substring) |
|5   | [Edit Operations](#edit-operations) |
|6   | [Longest Increasing Subsequence](#longest-increasing-subsequence) |
|7   | [Subsequence and Subarray Sum](#subsequence-and-subarray-sum) |
|8   | [Coin Change Problem](#coin-change-problem) |
|9   | [Optimal Binary Search Tree](#optimal-binary-search-tree) |
|10  | [Rod Cutting Problem](#rod-cutting-problem) |
|11  | [Wildcard Pattern Matching](#wildcard-pattern-matching) |
|12  | [Regular Expression Matching](#regular-expression-matching) |
|13  | [Egg Dropping Problem](#egg-dropping-problem) |
|14  | [Maximum sum rectangle in a 2D matrix ( 2D Kadane )](#maximum-sum-rectangle-in-a-2d-matrix--2d-kadane-) |
|15  | [Weighted Job Scheduling](#weighted-job-scheduling) |
|16  | [Maximum Sub Square With All 1 In Binary Matrix](#maximum-sub-square-with-all-1-in-binary-matrix) |
|17  | [Maximum Sub Rectangle With All 1 In Binary Matrix](#maximum-sub-rectangle-with-all-1-in-binary-matrix) |
|18  | [Maximum profit by buying and selling a share at most k times](#maximum-profit-by-buying-and-selling-a-share-at-most-k-times) |
|19  | [0-1 Knapsack](#0-1-knapsack) |
|20  | [Optimal Strategy Game Pick-up from end of the Array](#optimal-strategy-game-pick-up-from-end-of-the-array) |
|21  | [Minimum jump to reach end of array](#minimum-jump-to-reach-end-of-array) |
|22  | [Box Stacking Problem](#box-stacking-problem) |




##  Matrix Chain Multiplication
Given a sequence of matrices, find the most efficient way to multiply these matrices together. The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications.
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

ll matrixMultiplication()
{
  ll n;
  cin>>n;
  std::vector<pii> v;

  fr(i,0,n)
  {
    ll a,b; cin>>a>>b;
    v.pb(mp(a,b));
  }

  ll dp[n][n];

  fr(i,0,n) fr(j,0,n) dp[i][j]=INT_MAX;

  fr(i,0,n) dp[i][i]=0;

  fr(i,0,n)
  fr(j,i+1,n)
  fr(k,i,j)
  {
    dp[i][j]=min(dp[i][j],dp[i][k]+dp[k+1][j]+v[i].F*v[k].S*v[j].S);
  }

  return dp[0][n-1];


}

int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    cout<<matrixMultiplication();

    
   
    

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}

// Time Complexicity : O(n^3)
// Space Complexicity : O(n^2)

//Example
// Input         Output
// 5             70
// 1 2 
// 2 4
// 4 5
// 5 6
// 6 2
```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Longest Palindromic Subsequence

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

int longestPalindromicSubsequence(string s){
    int dp[s.size()][s.size()];
    for(int i = 0 ; i < s.size(); i++){
        dp[i][i] = 1;
    }
    for(int l = 1 ; l < s.size() ; l++){
        int i = 0, j = l;
        while(j != s.size()){
            if(s[i] == s[j]){
                dp[i][j] = 2 + dp[i+1][j-1];
            }
            else{
                dp[i][j] = max(dp[i+1][j],dp[i][j-1]);
            }
            i++;j++;
        }
    }
    return dp[0][s.size()-1];
}

int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s;
    cin>>s;

    cout<<longestPalindromicSubsequence(s);

    

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Time Complexicity : O(n^2)
// Space Complexicity : O(n^2)
//Example
// Input         Output
// asdfa           3
// iuabtsucsyftg   5
```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Longest Common Subsequence

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

int longestCommonSubsequence(string x,string y){
    int m = x.size(),n = y.size();
    int dp[m+1][n+1];
    for(int i=0;i<=m;i++){
        dp[i][0] = 0;
    }
    for(int j=0;j<=m;j++){
        dp[0][j] = 0;
    }
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++){
            if(x[i-1] == y[j-1]){
                dp[i][j] = dp[i-1][j-1]+1;
            }
            else{
                dp[i][j] = max(dp[i][j-1],dp[i-1][j]);
            }
        }
    }
    return dp[m][n];
}

int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s1,s2;
    cin>>s1>>s2;

    cout<<longestCommonSubsequence(s1,s2);

    

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Time Complexicity : O(n*m)
// Space Complexicity : O(n*m)
// Example
// Input            Output
// anshaj anuj        3
```

**[⬆ Back to Top](#----cp-algorithms-)** 


##  Longest Common Substring

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

int longestCommonSubstring(string x,string y){
    int m =  x.size();
    int n =  y.size();
    int dp[m+1][n+1];
    for(int i = 0 ; i < m; i++){
        dp[i][0] = 0;
    }
    for(int j = 0; j < n; j++){
        dp[0][j] = 0;
    }
    int ans=0;
    for(int i = 1; i <= m; i++){
        for(int j = 1; j <=n; j++){
            if(x[i-1] == y[j-1]){
                dp[i][j] = 1 + dp[i-1][j-1];
            }
            else{
                dp[i][j] = 0;
            }
            ans=max(dp[i][j],ans);
        }
    }
    return ans;
}

int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s1,s2;
    cin>>s1>>s2;

    cout<<longestCommonSubstring(s1,s2);


    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Time Complexicity : O(n*m)
// Space Complexicity : O(n*m)
// Example
// Input            Output
// anshaj anuj        2

```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Edit Operations

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

int editOperations(string s1, string s2){
    int m = s1.length();
    int n = s2.length();
    int dp[m+1][n+1];
    for (int i = 0; i <= m; i++) {
        dp[i][0] = i;
    }
    for (int j = 0; j <= n; j++) {
        dp[0][j] = j;
    }

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
        if (s1[i-1] == s2[j-1]) dp[i][j] = dp[i-1][j-1];
        else dp[i][j] = 1 + min(min(dp[i][j-1],dp[i-1][j]),dp[i-1][j-1]);
        }
    }
    return dp[m][n];
}

int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s1,s2;
    cin>>s1>>s2;

    cout<<editOperations(s1,s2);


    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Time Complexicity : O(n*m)
// Space Complexicity : O(n*m)
// Example
// Input            Output
// anshaj anuj        3

```

**[⬆ Back to Top](#----cp-algorithms-)** 

##  Longest Increasing Subsequence

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time complexicity: O(n^2) 
int longestIncreasingSubsequence(std::vector<ll> a,ll n){
     ll dp[n];
    for(int i=0;i<n;i++)
    dp[i]=1;
    ll ans=zer;
    for(int i=1;i<n;i++)
     for(int j=0;j<i;j++)
      {
      if(a[j]<a[i]) dp[i]=max(dp[i],dp[j]+1);
      ans=max(ans,dp[i]);
      }
      return ans;

}
// Time complexicity: O(nlogn) 
int longestIncreasingSubsequence2(std::vector<ll> v){
    if (v.size() == 0) 
        return 0; 
    std::vector<ll> a;
    a.pb(v[0]);
    ll length=1;
    fr(i,1,v.size())
    {
        if(a[length-1]<v[i])
            a.pb(v[i]);
        else 
        {
            int ind=lb(v,v[i]);
            a[ind]=v[i];
        }

            length=a.size();
    }
    return length; 
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    int n;
    cin>>n;
    std::vector<ll> a(n);
    for(int i=0;i<n;i++)
    cin>>a[i];
    
      cout<<longestIncreasingSubsequence(a,n)<<endl;
      cout<<longestIncreasingSubsequence2(a)<<endl;


    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Space Complexicity : O(n)
// Example
// Input            Output
// 7                    4
// 1 4 1 3 4 2 5        4

```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Subsequence and Subarray Sum

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n^2)
// Space Complexicity : O(n*k) 
// returns 1 if any subsequence having sum equal to k
int subsequenceSumProblem(std::vector<ll> a,ll k){
    int n=a.size();
     ll dp[n+1][k+1];
     memset(dp,0,sizeof(dp));
     fr(i,0,n+1) dp[i][0]=1;
     
     fr(i,1,n+1)
     {
        ll temp=a[i-1];
        fr(j,temp,k+1)
        {
            if(dp[i-1][j-temp]) dp[i][j]=1;
        }
     }
    
     return dp[n][k];

}
// Time complexicity: O(n) 
// Space Complexicity : O(n)
// returns no of subarray sum equals k (not subsequence)
int subarraySumProblem(std::vector<ll> v,ll k){
    int n=v.size();
    unordered_map<ll, ll> count; 
  
    int res = 0; 
    ll sum = 0; 
    fr(i,0,n) { 
        sum += v[i]; 
        if (sum == k)  
            res++;         
        if (count.find(sum - k) !=  
                                  count.end())  
            res += (count[sum - k]); 
        count[sum]++; 
    } 
  
    return res;
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    int n;
    cin>>n;
    std::vector<ll> a(n);
    for(int i=0;i<n;i++)
    cin>>a[i];
    
      cout<<subsequenceSumProblem(a,5)<<endl;
      cout<<subarraySumProblem(a,5)<<endl;


    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input            Output
// 7                    1
// 1 4 1 3 4 2 5        3

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  Coin Change Problem

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*k)
// Space Complexicity : O(n*k) 
// returns minimum no of coin needed for sum=k (infinite coins of each denomination)
int coinChangeProblem(std::vector<ll> a,ll k){
    int n=a.size();
     ll dp[n+1][k+1];
     memset(dp,0,sizeof(dp));
     fr(i,1,k+1) dp[0][i]=inf;

     
     fr(i,1,n+1)
     {
        ll temp=a[i-1];
        fr(j,1,k+1)
        {
            if(j<temp) dp[i][j]=dp[i-1][j];
            else
            {
            dp[i][j] = min(min(dp[i-1][j-temp],dp[i][j-temp])+1, dp[i-1][j]);
            }
        
        }
     }

     return dp[n][k];

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    int n;
    cin>>n;
    std::vector<ll> a(n);
    for(int i=0;i<n;i++)
    cin>>a[i];
    
      cout<<coinChangeProblem(a,4)<<endl;
      cout<<coinChangeProblem(a,11)<<endl;

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input            Output
// 7                    4
// 1 5 6 8              2


```
**[⬆ Back to Top](#----cp-algorithms-)** 



##  Optimal Binary Search Tree  

Given a sorted array keys[0.. n-1] of search keys and an array freq[0.. n-1] of frequency counts, where freq[i] is the number of searches to keys[i]. Construct a binary search tree of all keys such that the total cost of all the searches is as small as possible.

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

ll getSum(ll *sum,ll i,ll j)
{
    if(i>j) return 0;
    ll temp=sum[j];
    if(i>0) temp-=sum[i-1];
    return temp;
}

// Time Complexicity : O(n*n*n)
// Space Complexicity : O(n*n) 
// dp[i][j] means min possible value from i to j
// Here vector a is sorted if not use pair and sort using comparator
int optimalBinarySearchTree(std::vector<ll> a,std::vector<ll> freq){
    ll n=a.size();
     ll dp[n][n];
     memset(dp,0,sizeof(dp));
     fr(i,0,n) dp[i][i]=freq[i];

     ll cumFreq[n]={freq[0]};

     fr(i,1,n) cumFreq[i]=cumFreq[i-1]+freq[i];



     ll inc=1,i=0,j=1;
     
     while(inc<n)
     {
        i=0; j=i+inc;
        while(i<n&&j<n)
      {
          
            dp[i][j]=inf;
            for(int k=i;k<=j;k++)
            {
                ll leftSum=getSum(cumFreq,i,k-1);
                ll rightSum=getSum(cumFreq,k+1,j);

                ll temp=freq[k];
                if(leftSum>0) temp+=(dp[i][k-1]+leftSum);
                if(rightSum>0) temp+=(dp[k+1][j]+rightSum);
                dp[i][j]=min(dp[i][j],temp);
            }
            // cout<<i<<" "<<j<<" "<<dp[i][j]<<endl;
            i++; j++;
      }
      inc++;
     }


     return dp[0][n-1];

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    int n;
    cin>>n;
    std::vector<ll> a(n),freq(n);
    for(int i=0;i<n;i++)
    cin>>a[i];
    for(int i=0;i<n;i++)
    cin>>freq[i];
    
      cout<<optimalBinarySearchTree(a,freq)<<endl;

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input              Output
// 3
// 10 12 20             142
// 34 8 50         

// 4
// 10 12 16 21          26
// 4 2 6 3   


```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Rod Cutting Problem

Given a rod of length k inches arrays of prices of respective length is given. Determine the maximum value obtainable by cutting up the rod and selling the pieces.
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

ll getSum(ll *sum,ll i,ll j)
{
    if(i>j) return 0;
    ll temp=sum[j];
    if(i>0) temp-=sum[i-1];
    return temp;
}

// Time Complexicity : O(n*n)
// Space Complexicity : O(n*n) 
// dp[i][j] means min possible value from i to j
// Here vector a is sorted if not use pair and sort using comparator
int rodCuttingProblem(std::vector<ll> a,std::vector<ll> cost,ll k){
    ll n=a.size();
     ll dp[n+1][k+1];
     memset(dp,0,sizeof(dp));

     fr(i,1,n+1)
     {
        ll temp=a[i-1];
        // cout<<cost[i]<<endl;
        fr(j,1,k+1)
        {
            dp[i][j] = dp[i-1][j];
            if(j>=temp)
            {
                dp[i][j]=max(dp[i][j],dp[i][j-temp]+cost[i-1]);
            }
            // cout<<i<<" "<<j<<" "<<dp[i][j]<<endl;
        }
     }
     


     return dp[n][k];

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    int n;
    cin>>n;
    std::vector<ll> a(n),cost(n);
    for(int i=0;i<n;i++)
    cin>>a[i];
    for(int i=0;i<n;i++)
    cin>>cost[i];
    
    cout<<rodCuttingProblem(a,cost,5)<<endl;

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input              Output
// 4
// 1 2 3 4              12
// 2 5 7 8



```
**[⬆ Back to Top](#----cp-algorithms-)** 



##  Wildcard Pattern Matching
Given a text and a wildcard pattern, implement wildcard pattern matching algorithm that finds if wildcard pattern is matched with text. The matching should cover the entire text (not partial text).  

The wildcard pattern can include the characters ‘?’ and ‘\*’  
*  ‘?’ – matches any single character  
*  ‘\*’ – Matches any sequence of characters (including the empty sequence)  

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*k)
// Space Complexicity : O(n*k) 
int wildCardPatternMatching(string s,string p){
    ll n=s.size();
    ll k=p.size();
    ll dp[n+1][k+1];
    memset(dp,0,sizeof(dp));
      
    dp[0][0]=1;

    fr(i,1,k+1) if(p[i-1]=='*') dp[0][i]=dp[0][i-1];

    fr(i,1,n+1) dp[i][0]=0;

    fr(i,1,n+1)
    {
        char temp=s[i-1];
        fr(j,1,k+1)
        {
            if(p[j-1]=='*') dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
            else if(p[j-1]==temp||p[j-1]=='?') dp[i][j]=dp[i-1][j-1];
            // cout<<dp[i][j]<<" ";
        }
        // cout<<endl;
    }

     return dp[n][k];
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s,pattern;

    cin>>s>>pattern;
    
    cout<<wildCardPatternMatching(s,pattern)<<endl;

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input              Output
// xaylmz                1
// x?y*z

// baaabab               1
// *****ba*****ab

// baaabab               0
// a*ab



```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Regular Expression Matching

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.  

*  '.' Matches any single character.  
*  '*' Matches zero or more of the preceding element.  
*  The matching should cover the entire input string (not partial).  

>  https://leetcode.com/problems/regular-expression-matching/

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*k)
// Space Complexicity : O(n*k) 
int regularExpressionMatching(string s,string p){
    ll n=s.size();
    ll k=p.size();
    ll dp[n+1][k+1];
    memset(dp,0,sizeof(dp));
      
    dp[0][0]=1;

    fr(i,1,k+1) if(p[i-1]=='*') {if(i-2>=0) dp[0][i]=dp[0][i-2]; else dp[0][i]=1;}

    fr(i,1,n+1)  dp[i][0]=0;

    fr(i,1,n+1)
    {
        char temp=s[i-1];
        fr(j,1,k+1)
        {
            if(p[j-1]=='*') {
                dp[i][j] = dp[i][j - 2];
                    if (p[j-2] == '.' || p[j - 2] == s[i - 1]) {
                        dp[i][j] = dp[i][j] | dp[i - 1][j];
                    }
            }
            else if(p[j-1]==temp||p[j-1]=='.') dp[i][j]=dp[i-1][j-1];
            // cout<<dp[i][j]<<" ";
        }
        // cout<<endl;
    }

     return dp[n][k];
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    string s,pattern;

    cin>>s>>pattern;
    
    cout<<regularExpressionMatching(s,pattern)<<endl;  //regEx

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input              Output
// mississippi            0
// mis*is*p*.

// ab                     1
// .*

```

**[⬆ Back to Top](#----cp-algorithms-)** 


##  Egg Dropping Problem
Suppose that we wish to know which stories in a n-story building are safe to drop eggs from, and which will cause the eggs to break on landing. We make a few assumptions:

*  An egg that survives a fall can be used again.
*  A broken egg must be discarded.
*  The effect of a fall is the same for all eggs.
*  If an egg breaks when dropped, then it would break if dropped from a higher floor.
*  If an egg survives a fall then it would survive a shorter fall.
*  It is not ruled out that the first-floor windows break eggs, nor is it ruled out that the 36th-floor do not cause an egg to break.

>  You have n-floors and E eggs. Find minimum no of attempts needed in worst case.

![Egg Dropping Problem Concept](https://github.com/anshajsharma/CP-Algorithms/blob/master/Data/egg%20dropping.png)

>  My sol is in O(n^3) it can be reduced to O(N^2) using DAG(Directed Acyclic Graph)

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*n*e)
// Space Complexicity : O(n*e) 
ll eggDroppingProblem(ll n,ll e){
    ll dp[e+1][n+1];
    memset(dp,0,sizeof(dp));
    fr(i,0,e+1) fr(j,0,n+1) dp[i][j]=inf;
    fr(i,1,n+1) dp[1][i]=i;
    fr(i,0,e+1) dp[i][0]=0;

    fr(i,2,e+1)
    {
        fr(j,1,n+1){
            fr(x,1,j+1)
            {
                ll temp=max(dp[i][j-x],dp[i-1][x-1]);
                dp[i][j]=min(dp[i][j] , temp + 1 );
            }
        }
    } 

     return dp[e][n];
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    ll n,e;

    cin>>n>>e;
    
    cout<<eggDroppingProblem(n,e)<<endl;  //regEx

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input              Output
// 10 2                 4

// 36 2                 8
```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Maximum sum rectangle in a 2D matrix ( 2D Kadane )
Given a 2D array, find the maximum sum subarray in it.
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*n*n)
// Space Complexicity : O(n) 
ll maximumSumRectangularSubmatrix(ll n){
    ll a[n][n];
    fr(i,0,n) fr(j,0,n) cin>>a[i][j];

    ll mxL,mxUp,mxDn,mxR;
    ll b[n];
    ll mxSum=zer,currMax=zer,currSum=0;

    fr(L,0,n)
    {
         memset(b,0,sizeof(b));
         fr(R,L,n)
         {

            fr(j,0,n) {
                b[j]+=a[j][R]; 
            }


            currMax=zer;
            currSum=0;

            ll stPoint=0;

            fr(i,0,n)
            {
                currSum+=b[i];
                if(currMax<currSum){
                    currMax=currSum;
                    if(currMax>mxSum){
                    mxSum=currMax;
                    mxL=L;
                    mxR=R;
                    mxUp=stPoint;
                    mxDn=i;
                }
                }
                
                if(currSum<0) {currSum=0; stPoint=i+1;}
            }


         }
    }
             cout<<mxSum<<" " <<mxL<<" "<<mxR<<" "<<mxUp<<" "<<mxDn<<endl;



     

    return mxSum;
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    ll n;

    cin>>n;

    
    cout<<maximumSumRectangularSubmatrix(n)<<endl;  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                  Output

// 3
// 5 4 3                14 0 2 0 1
// 2 -2 2               14
// 5 -6 -9

// 5
// 1 2 -1 -4 -20        29 1 3 1 3
// -8 -3 4 2 1          29
// 3 8 10 1 3
// -4 -1 1 7 -6
// -1 -1 -1 -1 -1

```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Weighted Job Scheduling
Given N jobs where every job is represented by following three elements of it.

1.  Start Time
2.  Finish Time
3.  Profit or Value Associated (>= 0)  

Find the maximum profit subset of jobs such that no two jobs in the subset overlap.

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

struct Job {
    ll stTime,endTime,profit;
};

bool comp(Job job1,Job job2)
{
    if(job1.endTime!=job2.endTime) return job1.endTime<job2.endTime;
    else return job1.stTime<job2.stTime;
}

// Time Complexicity : O(n*n)
// Space Complexicity : O(n*n) 
ll weightedJobScheduling(){
       ll n;
       cin>>n;
       Job jobs[n]; 
       fr(i,0,n)
       {
        ll a,b,c;
        cin>>a>>b>>c;
        jobs[i].stTime=a;
        jobs[i].endTime=b;
        jobs[i].profit=c;
       }
       sort(jobs,jobs+n,comp);
       ll dp[n]={0};
       fr(i,0,n)
       {
        dp[i]=jobs[i].profit;
       }


       fr(i,1,n)
       {
        fr(j,0,n)
        {
            if(jobs[i].stTime>=jobs[j].endTime)
            {
                dp[i]=max(dp[i],dp[j]+jobs[i].profit);
            }
        }
       }

       ll mx=zer;
       fr(i,0,n) mx=max(dp[i],mx);
       return mx;
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    cout<< weightedJobScheduling();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                  Output

// 6                        17
// 1 3 5
// 2 5 6
// 4 6 5
// 6 7 4
// 5 8 11 
// 7 9 2

// 5                        11
// 1 2 5
// 2 4 6
// 1 3 5
// 1 5 4
// 2 5 6

```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Maximum Sub Square With All 1 In Binary Matrix
Given a binary matrix, find out the maximum size square sub-matrix with all 1s.
*  https://leetcode.com/problems/maximal-square/
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;


// Time Complexicity : O(n*m)
// Space Complexicity : O(n*m) 
ll maxSubSquare(){
       ll n,m;
       cin>>n>>m;
       ll a[n][m];

       fr(i,0,n)
       fr(j,0,m) cin>>a[i][j];

       ll dp[n+1][m+1];
       memset(dp,0,sizeof(dp));
       ll mx=zer;
       fr(i,1,n+1)
       fr(j,1,m+1)
       {
        if(a[i-1][j-1]==1)
        {
            dp[i][j]= min(min(dp[i-1][j-1],dp[i-1][j]),dp[i][j-1])+1;
        }
        mx=max(mx,dp[i][j]);
       }

       return mx;
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    cout<< maxSubSquare();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                    Output

// 5 4                         2
// 1 0 1 0
// 1 1 1 0
// 1 1 0 1
// 1 1 1 0
// 1 1 1 0

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  Maximum Sub Rectangle With All 1 In Binary Matrix
Given a binary matrix, find the maximum size rectangle binary-sub-matrix with all 1’s.
>  **Additional Concept Used:** Max Area under histogram.(stack) 
*  https://leetcode.com/problems/largest-rectangle-in-histogram/
```c++
int largestRectangleArea(vector<int>& a) {
        int ans=0;
        int n=a.size();
        stack<int> s;
        fr(i,0,n)
        {
            while(!s.empty()&&a[s.top()]>a[i])
            {
                int temp=s.top();
                s.pop();
                int t;
                if(s.empty()) t= a[temp]*i;
                else t = (i-s.top()-1)*a[temp] ;
                if(t>ans) ans=t;
            }
            s.push(i);
        }
        while(!s.empty())
            {
                int temp=s.top();
                s.pop();
                int t;
                if(s.empty()) t= a[temp]*n;
                else t = (n-s.top()-1)*a[temp] ;
                if(t>ans) ans=t;
            }
        return ans;
        
    }
```

*  https://leetcode.com/problems/maximal-rectangle/
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*m)
// Space Complexicity : O(n*m) 
void maxSubRectangle(){
       ll n,m;
       cin>>n>>m;
       ll a[n][m];

       fr(i,0,n)
       fr(j,0,m) cin>>a[i][j];

       ll mx=zer;
       ll currMax=zer,currSum=0;
       ll mxL=0,mxUp=0,mxDn=0,mxR=0;

       ll b[n];
       fr(L,0,m)
        {
         memset(b,0,sizeof(b));
         fr(R,L,m)
         {
            fr(j,0,n) {
                if(a[j][R]) b[j]+=1;
                else b[j]=0;
            }

            currMax=zer;
            currSum=0;
            stack<ll> s;
            ll stPoint=0;

            fr(i,0,n)
            {
                while(!s.empty() && b[s.top()]>b[i])
                {
                    stPoint=s.top();
                    s.pop();
                    currSum= (i- stPoint)*b[stPoint];
                    if(currMax<currSum){
                         currMax=currSum;
                         if(currMax>mx){
                         mx=currMax;
                         mxL=L;
                         mxR=R;
                         mxUp=stPoint;
                         mxDn=i;
                        }
                    }
                }
                s.push(i);
            }
            while(!s.empty()){
                stPoint=s.top();
                    s.pop();
                    if(s.empty()) currSum= (n)*b[stPoint];
                    else currSum= (n - stPoint)*b[stPoint];
                    if(currMax<currSum){
                         currMax=currSum;
                         if(currMax>mx){
                         mx=currMax;
                         mxL=L;
                         mxR=R;
                         mxUp=stPoint;
                         mxDn=n-1;
                        }
                    }
            }


         }
    }
     cout<<mx<<" " <<mxL<<" "<<mxR<<" "<<mxUp<<" "<<mxDn<<endl;

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    maxSubRectangle();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                     Output

// 5 4                      8 0 1 1 4
// 1 0 1 0
// 1 1 1 0
// 1 1 0 1
// 1 1 1 0
// 1 1 1 0

// 5 5                      10 0 4 3 4
// 1 0 1 0 1
// 1 1 1 0 1
// 1 1 0 1 1
// 1 1 1 1 1
// 1 1 1 1 1


```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Maximum profit by buying and selling a share at most k times
In share trading, a buyer buys shares and sells on a future date. Given the stock price of n days, the trader is allowed to make at most k transactions, where a new transaction can only start after the previous transaction is complete, find out the maximum profit that a share trader could have made.
>  **Note:** if k is *unlimited* then stack is used.  

*  https://leetcode.com/problems/best-time-to-buy-and-sell-stock/  *
*  https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/  
*  https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/  
*  https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/   (reduce space complexicity to o(n) using dp[2][n])
```C++

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*k)
// Space Complexicity : O(n*k) 
void maxProfit(){
       ll n,k;
       cin>>n>>k;

       ll a[n];
       fr(i,0,n) cin>>a[i];

       ll dp[k+1][n];
       memset(dp,0,sizeof(dp));
       
       ll maxDiff=zer;

       fr(i,1,k+1)
       {
        maxDiff=zer;
        fr(j,1,n)
        {
            maxDiff=max(maxDiff,dp[i-1][j-1]-a[j-1]);
            dp[i][j]=max(dp[i][j-1],a[j]+maxDiff);
        }
       }

       cout<<dp[k][n-1]<<endl;
       

        

}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    maxProfit();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                     Output

// 6 2                         87
// 10 22 5 75 65 80


// 5 1                         0
// 7 6 4 3 1

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  0-1 Knapsack
Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights associated with n items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. You cannot break an item, either pick the complete item or don’t pick it (0-1 property).

>  https://leetcode.com/problems/partition-equal-subset-sum/  
>  https://leetcode.com/problems/partition-to-k-equal-sum-subsets/ (NP Hard)
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n*k)
// Space Complexicity : O(n*k) 
void maxProfit(){
        ll n,k;
        cin>>n>>k;
        ll wt[n],profit[n];
        fr(i,0,n) cin>>wt[i];
        fr(i,0,n) cin>>profit[i];

        ll dp[n+1][k+1];
        memset(dp,0,sizeof(dp));

        fr(i,1,n+1)
        {
            ll temp=wt[i-1];
            fr(j,0,k+1)
            {
                if(j-temp<0) dp[i][j]=dp[i-1][j];
                else dp[i][j]=max( max(dp[i][j-1], dp[i-1][j] ),dp[i-1][j-temp]+profit[i-1]);
            }
        }
        cout<<dp[n][k];


}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    maxProfit();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                     Output

// 4 7                         9
// 1 3 4 5
// 1 4 5 7


```
**[⬆ Back to Top](#----cp-algorithms-)** 


##  Optimal Strategy Game Pick-up from end of the Array
Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.  
  

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.  
*  https://leetcode.com/problems/predict-the-winner/
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define loop(i,n)    for(int i = 0; x < n; i++)
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

ll getSum(ll *sum,ll i,ll j)
{
    if(i>j) return 0;
    ll temp=sum[j];
    if(i>0) temp-=sum[i-1];
    return temp;
}

// Time Complexicity : O(n*n)
// Space Complexicity : O(n*n) 
void maxProfit(){
        ll n;
        cin>>n;

        ll a[n];
        fr(i,0,n) cin>>a[i];

        ll cumFreq[n]={a[0]};

        fr(i,1,n) cumFreq[i]=cumFreq[i-1]+a[i];


        ll dp[n+1][n+1];
        memset(dp,0,sizeof(dp));

        fr(i,1,n+1) dp[i][i]=a[i-1];

        ll inc=1,i=0,j=1;

     
     while(inc<n)
     {
        i=1; j=i+inc;
        while(i<n+1&&j<n+1)
        {
            dp[i][j]=max( 
                getSum(cumFreq,i-1,j-2)-dp[i][j-1]+a[j-1] , 
                getSum(cumFreq,i,j-1)-dp[i+1][j]+a[i-1]
                );
            i++; j++;
        }
        inc++;
     }

     // fr(i,0,n+1) {
     //    fr(j,0,n+1) cout<< dp[i][j]<<" ";
     //    cout<<endl;
     // }


     cout<<dp[1][n]<<" ";

     bool ans=dp[1][n]>=getSum(cumFreq,0,n-1)-dp[1][n];;

     cout<<ans<<endl;

      // return dp[1][n]>=getSum(cumFreq,0,n-1)-dp[1][n]; (if player 1 is winner return true)
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    maxProfit();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}
// Example
// Input                     Output

// 4                          10 1
// 7 1 3 4

// 3                          3 0 
// 1 5 2

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  Minimum jump to reach end of array

>  https://leetcode.com/problems/jump-game/  
>  https://leetcode.com/problems/jump-game-ii/  
>  https://leetcode.com/problems/jump-game-iii/
```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fr(i,j,n)   for(ll i=j;i<n;i++)
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)        lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)        upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long mod=pow(10,9)+7;

// Time Complexicity : O(n)
// Space Complexicity : O(n) 
void jump(){
        ll n;
        cin>>n;

        ll a[n];
        fr(i,0,n) cin>>a[i];

        ll jumpsCount[n],path[n];
        memset(jumpsCount,0,sizeof(jumpsCount));
        path[0]=-1;
        int i=0,j=0;
        while(j<n)
        {
            ll temp=i+a[i]-j+1;
            while(temp>0 && j<n )
            {  
                if(j){
                jumpsCount[j]=jumpsCount[i]+1;
                path[j]=i;
                }
                j++;
                temp--;
            }
            i++;
        }
        fr(i,0,n) cout<<jumpsCount[i]<<" "; 
        cout<<endl;
        fr(i,0,n) cout<<path[i]<<" ";
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    jump();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}

// Example
// Input                               Output
// 10                            0 1 1 2 2 3 3 4 4 4 
// 2 3 1 1 2 4 2 0 1 1          -1 0 0 1 1 4 4 5 5 5 
// In this example minimum jump required to reach at end of array from starting index is 4

```
**[⬆ Back to Top](#----cp-algorithms-)** 

##  Box Stacking Problem
You are given a set of n types of rectangular 3-D boxes, where the i^th box has height h(i), width w(i) and depth d(i) (all real numbers). You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.  
  
>  https://practice.geeksforgeeks.org/problems/box-stacking/1  
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
#define scn(n)       scanf("%lld",&n)
#define lscn(n)      scanf("%lld",&n)
#define lpri(n)      printf("%lld",n)
#define pri(n)       printf("%d",n)
#define pln()        printf("\n")
#define priln(n)     printf("%d\n",n)
#define lpriln(n)    printf("%lld\n",n)
#define srt(v)       sort(v.begin(),v.end())
#define srte(v)      sort(v.rbegin(),v.rend())
#define maxx         1000005
#define lb(v,n)      lower_bound(v.begin(),v.end(),n)-v.begin()
#define ub(v,n)      upper_bound(v.begin(),v.end(),n)-v.begin()
#define inf          LONG_MAX
#define zer          LONG_MIN
const long           mod=pow(10,9)+7;

struct box{
    ll l,w,h;
    void set(ll l,ll w,ll h)
    {
        this->l=l;
        this->w=w;
        this->h=h;
    }
};

bool comp(box a,box b)
{
    return a.l * a.w > b.l * b.w;
}

// Time  Complexicity : O(n*n)
// Space Complexicity : O(n) 
void boxStacking(){
        ll n;
        cin>>n;
        box boxes[3*n];

        fr(i,0,n) {
            ll a,b,c;
            cin>>a>>b>>c;
            ll ind=3*i;
            boxes[ind].set(max(a,b),min(a,b),c) ;
            boxes[ind+1].set(max(c,b),min(c,b),a) ;
            boxes[ind+2].set(max(a,c),min(a,c),b) ;
        }
        sort(boxes,boxes+3*n,comp);
        fr(i,0,3*n){
            cout<<boxes[i].l<<" "<<boxes[i].w<<" "<<boxes[i].h<<endl;
        }

        ll height[3*n],st[3*n];
        memset(height,0,sizeof(height));
        memset(st,-1,sizeof(st));
        
        fr(i,0,3*n) height[i]=boxes[i].h;
        
        fr(i,0,3*n){
            fr(j,i+1,3*n){
                if( boxes[i].l > boxes[j].l && boxes[i].w > boxes[j].w ) {
                    if( boxes[j].h + height[i] > height[j] ){
                        height[j]=boxes[j].h + height[i];
                        st[j]=i;
                    }
                }
            }
        }
        ll ans=0;
        fr(i,0,3*n){
            ans=max(ans,height[i]);
            cout<<height[i]<<" "; 
        }
        cout<<endl;
        fr(i,0,3*n){
            cout<<st[i]<<" "; 
        }
        cout<<endl;
        cout<<ans<<endl;
}
int main()
{
    // fast;
    #ifndef ONLINE_JUDGE
    freopen("inputf.in" , "r" , stdin);
    freopen("outputf.in" , "w" , stdout);
    #endif

    boxStacking();  

    #ifndef ONLINE_JUDGE
    cout<<"\nTime Elapsed: " << 1.0*clock() / CLOCKS_PER_SEC << " sec\n";
    #endif
    return 0;
}

// Example
// Input                      Output
// 4
// 4 6 7                       60
// 1 2 3
// 4 5 6
// 10 12 32

// 2                           11
// 1 2 4
// 3 2 5



```
**[⬆ Back to Top](#----cp-algorithms-)** 


