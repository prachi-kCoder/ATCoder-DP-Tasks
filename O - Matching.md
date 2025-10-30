# O - Matching

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7 ;

vector<vector<ll>> mat ;
vector<vector<ll>> dp ;
ll n ; ll full_msk ;
ll solve(ll man , ll mask ) {
    if (man >= n) return mask == full_msk ;// ie all women paired
    
    if (dp[man][mask] != -1LL) {
        return dp[man][mask] ;
    }
    
    ll cnt = 0LL ;
    for ( ll w = 0 ; w < n ; w++ ) {
        if (mat[man][w] == 1 && !(mask&(1<<w)) ){
            ll nxt_mask = (mask|(1<<w));
            cnt = (cnt + solve(man+1 , nxt_mask))%mod ;
        }
    }
    
    return dp[man][mask] = cnt ;
}
int main() {
    cin >> n ;
    full_msk = (1LL<<n)-1 ;
    
    mat.resize(n, vector<ll>(n));
    dp.resize(n , vector<ll>(full_msk + 1 , -1LL)) ;
    bool invalid = false ;
    for (ll i = 0; i < n ; i++) {
        bool no_pair = true ;
        for (ll j = 0; j < n ; j++) {
            cin >> mat[i][j] ;
            if (mat[i][j] == 1) {
                no_pair = false ;
            }
        }
        if (no_pair) {
            invalid = true ;
        }
    }
    if (invalid) {
        cout << 0 << endl ;
        return 0 ;
    }
    bool mask = 0LL ;
    ll ways = solve( 0 , mask ) ;// man[0-n-1]
    cout << ways << endl ;
    
    return 0;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY | 🧩 EXPLANATION |
|-----------|---------------|----------------|
| 🧭 TIME    | O(N × 2ⁿ)     | Each man explores 2ⁿ mask states, each visited once due to memoization |
| 🧠 SPACE   | O(N × 2ⁿ)     | DP table stores results for each (man, mask) pair |

