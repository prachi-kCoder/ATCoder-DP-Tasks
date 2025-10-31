# U-Grouping

- `Submask DP` :
#### What is asked is  :"the maximum total score you can get by partitioning all $N$ items into one or more groups?"
- Score is calculated within groups. If items {0, 1, 2} are in a group, the score is `a[0][1]` + `a[0][2]` + `a[1][2]`
-  If you partition into `{0, 1}` and `{2}`, the score is `a[0][1]`
-  The DP State: `dp[mask]` : The maximum score you can get by partitioning only the items present in mask.

-  Eg :dp[10110] would store the best possible score from partitioning items {1, 2, 4}
-  Possibility of partitioning :This could be:

- {1, 2, 4} (one group)
- {1, 2}, {4} (two groups)
- {1, 4}, {2} (two groups)
- {1}, {2, 4} (two groups)
- {1}, {2}, {4} (three groups)

- We want to calculate dp[mask] (the best way to partition the items in mask). How do we do this?
- `dp[mask] = max(dp[mask] , dp[mask^sub] + gp_score[sub]) ;`
- The best way to group items in mask is the maximum of (the score of putting group sub together) + (the best way to group all the rest of the items) ... over all possible choices for sub
- `dp[mask^sub]`: This is the optimal score for partitioning all the remaining items. We've already computed this value because mask^sub is smaller than mask
- `sub`: The mask representing a single group we are trying to form
  
```cpp

#include <bits/stdc++.h>
using namespace std;
#define ll long long
vector<vector<ll>> a ;

int main() {
    ll n ;
    cin >> n ;
    a.resize(n, vector<ll>(n)) ;
    for (ll i = 0; i < n ; i++) {
        for (ll j = 0; j < n; j++) {
            cin >> a[i][j] ;
        }
    }
    vector<ll> gp_score((1<<n),0LL) ;
    for (ll mask = 0 ; mask < (1<<n) ; mask++) {
        ll sc = 0LL ;
        for (ll i = 0 ; i < n ; i++) {
            if (mask&(1<<i)) {
                for (ll j = i+1 ; j < n ; j++) {
                    if (mask&(1<<j)) {
                        sc += a[i][j] ;
                    }
                }  
            }
        }
        gp_score[mask] = sc ;
    }
    
    vector<ll> dp((1<<n), 0LL) ;
    ll mx = 0LL ;
    for (ll mask = 0 ; mask < (1<<n) ; mask++) {
        for (ll sub = mask ; sub ; sub = ((sub-1) & mask)) {
            // making partition within the mask 
            dp[mask] = max(dp[mask] , dp[mask^sub] + gp_score[sub]) ;
        }
        mx = max(dp[mask] , mx) ;
    }
    cout<< mx << endl ;
    
    return 0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |       O(3^N) DP Calculation (dp): This is the submask enumeration loop you mentioned. The total number of operations for this part is sum{k=0}^{N} {N}C{k}. 2^k = (1 + 2)^N = 3^N     |  Exponential as all mask and all submask of every mask [0- 2^N]  are computed for mx score of partitioning|
| 🧠 SPACE |    O(2^N)        | Keeping mx score of all different masks             |
