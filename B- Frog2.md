# B-FROG 2

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
        ll n , k ;
        cin >> n >> k;
        vector<ll> h(n);
        for (ll &x : h) {
            cin >> x ;
        }
        vector<ll> dp(n, LLONG_MAX);
        dp[0] = 0LL ;
        for (ll i = 1 ; i < n ; i++) {
            for (ll j = max(0LL , i-k) ; j < i ; j++) {
                dp[i] = min(dp[i] , dp[j] + abs(h[j] - h[i])) ;
            }
        }
        
        cout << dp[n-1] << endl ;
 
    
    return  0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(N x K)         | All k prev possible for all i [0,N-1] indices          |
| 🧠 SPACE |      O(N X K)      |      Dp table      |
