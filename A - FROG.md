# A-FROG 

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
int main() {
    
        ll n ;
        cin >> n ;
        vector<ll> h(n);
        for (ll i = 0; i < n ; i++) {
            cin >> h[i] ;
        }
        vector<ll> dp(n, LLONG_MAX);
        ll prev2 = 0LL ;
        ll prev1 = abs(h[1] - h[0]) ;
        
        for (ll i = 2 ; i < n ; i++) {
            ll curr = min( prev1 + abs(h[i] - h[i-1]) , prev2 + abs(h[i] - h[i-2])) ;
            
            prev2 = prev1 ;
            prev1 = curr ;
        }
        cout << prev1 << endl ;
 
    
    return  0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(N )   | For all i [0,N] are to be computed using i-1, i-2 |
| 🧠 SPACE |      O(1)     |   Only prev1, prev2 are req         |
