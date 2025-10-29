# L-Deque

- Consider taking it as maximising the diff : ie X-Y maximisatoin , Y-X maximisation
  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
ll dp[3001][3001] ;// score of X-Y {l,r}

// both tries to maximise their own score so that for taro [l,r] increases and for jiro [l,r] -> decreases 
ll solve(ll l , ll r , vector<ll>& a ) {
    if (l > r) return 0LL ;
    if (dp[l][r] != -1LL) return dp[l][r];
    ll pick_left = a[l] - solve(l+1 , r , a) ;
    ll pick_right = a[r] - solve(l , r-1 , a) ;
    
    return dp[l][r] = max(pick_left , pick_right) ;
}
int main() {
    // ll t ;
    // cin >> t ;
    // while (t-- > 0) {
        ll n ; 
        cin >> n ;
        vector<ll> a(n) ;
        
        // deque<ll> dq ;
        for (ll i = 0 ; i < n ; i++) {
            cin >> a[i] ;
            // dq.push_back(a[i]) ;
        }
        memset(dp , -1LL , sizeof(dp)) ;
        
        ll sc = solve(0 , n-1 ,  a) ;
        // print(n) ;
        cout << sc << endl ;
    // }

}

```
