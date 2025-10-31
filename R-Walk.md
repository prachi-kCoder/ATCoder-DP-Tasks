# R-Walk

- Matrix exponentiation : May not be your first apporach if not familiar with this concept .
### WHY MATRIX EXPO ?
Let’s say you have an adjacency matrix 
𝐴 of a graph:𝐴[𝑖][𝑗]= number of direct edges from node 𝑖→𝑗
Now, when you multiply two matrices:
(𝐴2)[𝑖][𝑗]=∑𝑘𝐴[𝑖][𝑘]⋅𝐴[𝑘][𝑗]

This counts the number of length-2 walks from 𝑖→: go from 𝑖→𝑘→𝑗
So in general:
(𝐴𝐾)[𝑖][𝑗]= number of walks of length 𝐾
 from node 𝑖→𝑗


- HENCE , You don’t need to simulate paths or detect cycles. Matrix exponentiation automatically counts all valid walks, including cyclic and repeated ones, because it’s just multiplying transition possibilities.
- 
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7;
ll n ;
vector<vector<ll>> mat_mul(vector<vector<ll>>& a,vector<vector<ll>>& b ) {
    vector<vector<ll>> c( n, vector<ll>(n , 0LL)) ;
    
    for (ll i = 0; i < n ; i++) {
        for (ll j = 0; j < n ; j++) {
            for (ll k = 0; k < n ; k++) {
                c[i][j] = (c[i][j] + (a[i][k] * b[k][j])%mod ) %mod ;
            }
        }
    }
    return c ;
}
vector<vector<ll>> mat_expo(vector<vector<ll>>& base , ll expo) {
    vector<vector<ll>> res( n, vector<ll>(n , 0)) ;
    for (ll i = 0 ; i<n ; i++) res[i][i] = 1LL ;
    while (expo > 0) {
        if (expo&1) res = mat_mul(res , base);
        base = mat_mul(base , base) ;
        expo >>= 1 ;
    }
    return res ;
}
int main() {
    ll  k;
    cin >> n >> k ;
    vector<vector<ll>> A(n,vector<ll>(n)) ;
    for (ll i = 0 ;i < n ; i++) {
        for (ll j = 0 ;j < n ; j++) {
            cin >> A[i][j] ;
        }
    }
    vector<vector<ll>> ak = mat_expo(A, k) ;
    ll ans = 0LL ;
    for (ll i = 0 ;i < n ; i++) {
        for (ll j = 0 ;j < n ; j++) {
            ans = (ans + ak[i][j])%mod ;
        }
    }
    cout << ans << endl ;
}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N^3 X logK)      |  N^3 -> Matrix multiplication , logN as while mat_expo (the order n -> n/2-> n/4 -> n/8 ->....  so total logN levels of expo while loop)          |
| 🧠 SPACE |   O(N X N)         |    O(N X N)         |
