## C - Vacation

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
        ll n  ;
        cin >> n ;
        vector<vector<ll>> p(n, vector<ll>(3));
        
        for (ll i = 0 ; i < n ; i++) {
            for (ll j = 0; j < 3 ; j++) {
                cin >> p[i][j] ;
            }
        }
        // vector<vector<ll>> dp(n, vector<ll>(3,0LL)) ;
        ll ap = p[0][0];
        ll bp = p[0][1];
        ll cp = p[0][2];
        
        for (ll i = 1 ; i < n ; i++) {
            ll a , b, c ;
            a = p[i][0] + max(bp , cp);
            b = p[i][1] + max(ap , cp);
            c = p[i][2] + max(ap , bp);
            ap = a , bp = b , cp = c ;
        }
        
        cout << max({ ap, bp, cp }) << endl ;
 
    
    return  0 ;
}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)   |  Consider all 3 possible of 3 choices at every index         |
| 🧠 SPACE |    O(1)       | Keeping only prev state values is enough no extra space needed           |
