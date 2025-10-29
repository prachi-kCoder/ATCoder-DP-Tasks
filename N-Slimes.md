# N - SLIMES

- Here for len = 1 , no combination cost is to be taken as no cost for the single element ,
- The dp[i][j] -> Min cost for combining the complete range(i,j) .

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
vector<vector<ll>> dp ;

int main() {
    // ll t ;
    // cin >> t ;
    // while (t-- > 0) {
        ll n ;
        cin >> n ;
        dp.resize(n , vector<ll>(n)) ;
        vector<ll> a(n) ;
        vector<ll> pre(n+1) ;
        for (ll i = 0 ; i < n ; i++) {
            cin >> a[i] ;
            pre[i+1] = a[i] + pre[i] ;
        }
        
        for (ll len = 2 ; len <= n ; len++ ) {
            for (ll i = 0 ; i <= n-len ; i++) {
                ll j = i + len - 1 ;
                dp[i][j] = LLONG_MAX ;
                for (ll k = i  ; k < j ; k++) {
                    ll cost = dp[i][k] + dp[k+1][j] + pre[j+1] - pre[i] ;
                    
                    dp[i][j] = min(dp[i][j] , cost);
                }
            }
        }
      
        cout << dp[0][n-1] << endl ;
    // }

}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N x N x N)   |  Dp table is for the right splits k b/w i , j-1   |
| 🧠 SPACE |   O(N x N)         |   Dp table used          |

