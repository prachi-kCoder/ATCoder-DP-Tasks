# COINS :
- `Dp[i][j]` : State gives the Prob of getting j heads out of i coins  (obviously i >= j)
- Init : dp[0][0] = 1.0 As for no coins -> 100% gurantee of no heads
- `Dp[i][j]` = `Prob_from_getting_head` + `Prob_getting_tail`
-   `Prob_from_getting_head` = dp[i-1][j-1]*Head_prob  {Ie in i-1 we had j-1 heads and got jth head now } here (j > 0)
-   `Prob_from_getting_tail` = dp[i-1][j]*Tail_prob  {Ie we already had j heads from i-1 coins as jth->Tail }

```cpp
#include <bits/stdc++.h>
#include <iomanip>
using namespace std;
#define ll long long

int main() {
    int n; // ll is not needed for n <= 2999
    cin >> n;
    
    vector<double> p(n);
    for (int i = 0; i < n; i++) {
        cin >> p[i];
    }
    
    vector<vector<double>> dp(n+1 , vector<double>(n+1 , 0.0)) ;
    dp[0][0] = 1.0 ;
    
    
    for (int i = 1; i <= n ; i++) {
        double hp = p[i-1] ;
        double tp = 1.0-p[i-1] ;
        
        for (int j = 0 ; j <= i ; j++) {
            double prob_from_tails = (dp[i-1][j]*tp) ;
            double prob_from_heads = 0.0 ;
            if (j > 0) { // as no_head -> no Prob from heads from ith coin 
                prob_from_heads = (dp[i-1][j-1]*hp) ;      
            }
            dp[i][j] = prob_from_heads + prob_from_tails ;
        }
    }

    double ans = 0.0 ;
    int mn_heads = (n+1)/2 ;
    for (int j = mn_heads ;  j <= n ; j++) {
        ans += dp[n][j] ;
    }
    
    cout << fixed << setprecision(10) << ans << endl ;

}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N x N)       |  For n coins , n heads are possible         |
| 🧠 SPACE |   O(N X N)         |  Dp table          |
