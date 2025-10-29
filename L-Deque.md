# L-Deque

- Consider taking it as maximising the diff : ie X-Y maximisatoin , Y-X maximisation


# Tabulation :
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
ll dp[3001][3001] ;// score of X-Y {l,r}

void print (ll n) {
    
    for (ll i = 0 ; i < n ; i++) {
        for (ll j = 0 ; j < n ; j++) {
            cout << dp[i][j] << " " ;
        }
        cout << endl ;
    }
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
        memset(dp, 0LL, sizeof(dp));
        
        // len = 1 ;
        for (int i = 0 ; i < n ; i++) {
            dp[i][i] = a[i] ;
        }
      
        for (ll len = 2 ; len <= n ;len++) {
            for (int l = 0; l <= n-len ; l++) {
                ll r = l + len - 1 ;
                dp[l][r] = max(a[l] - dp[l+1][r] , a[r] - dp[l][r-1]);
            }
        }
        // print(n) ;
        cout << dp[0][n-1] << endl ;
    // }

}
```

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

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(N x N)    |  For all (l,r ) |
| 🧠 SPACE |     O(N X X)       |  Dp table           |
