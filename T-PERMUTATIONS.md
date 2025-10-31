# T-PERMUTATIONS

- Here DP state means `dp[i][j]` : Count of permuation of numbers[1-i] ending at a num = j and i goes from [1, N] and j goes from [1,i]  
- Now we also have constraints over the any ith index from string s `>` or `<`  from any range [1,i] nums : `s[i-1]` conditions are to be satisfies for sure
- Now use k {intermediate compute the next state } dp[i][j] using dp[i-1][j]  , do take care fo condition applied from s[i] .

- The `i-th` element `p_i` is placed, and we look at the `(i-1)`-th element `p_{i-1}`. The constraint between them is s[i-2].
- In our relative-rank DP, this means the previous permutation `(p_1, ..., p_{i-1})` must have ended in a number `k` that is less than `j`
- So, dp[i][j] is the sum of all dp[i-1][k] where k < j.

- `s[i-2] == '>'` : dp[i][j] is the sum of all dp[i-1][k] where j <= k <= i-1 .


```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;
#define ll long long
// We need N+1, but adding a little buffer is safe.
const int MAXN = 3005; 
const ll MOD = 1e9 + 7;
ll dp[MAXN][MAXN];
ll prefix_sum[MAXN] ;

int main() {
	ll n;
    cin >> n;
    string s;
    cin >> s;
    memset(dp , -1LL , sizeof(dp)) ;
    dp[1][1] = 1LL ;
    
    for (ll i = 2; i <= n ; i++) {
        prefix_sum[0] = 0 ;
        for (ll j = 1 ; j <= i-1 ; j++) {// sum for i-1 th row 
            prefix_sum[j] = (prefix_sum[j-1] + dp[i-1][j])%MOD ;
        }
        ll total_sum = prefix_sum[i-1]; 
        char c = s[i-2] ;
        
        for (ll j = 1 ; j <= i ; j++) {// ending at any j value [1,i]
            if (c == '<') {
                // for all k < j {ie the sum of all permuations of sum < j}
                dp[i][j] = prefix_sum[j-1] ;// ie upto j-1)th tk ka sum
            }else {
                // for k >= j 
                ll sum_greater = (total_sum - prefix_sum[j-1] + MOD)% MOD;
                dp[i][j] = sum_greater ;
            }
        }
    }
    ll ans = 0LL ;
    for (ll j = 1 ; j <= n ; j++) {
        ans = (ans + dp[n][j])%MOD ;
    }
    cout << ans << endl ;
    
    return 0 ;
}

```
