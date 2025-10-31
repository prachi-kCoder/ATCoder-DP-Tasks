# S-DigitSum

### Complexicity Analysis :
- Here Space is to be maintained due to large values to be handled
- `dp[i][tight][is_lz][d_sum_mod_d]` :
- N : upto 100000 ,
- tight , is_leading_zero : 2 X 2
- d_sum%d -> at max be 99 {at digit sum is take mod with d {mx : 100}}


- Keep in mind neither int nor llong can handle such huge number `{10^10000}` hence get string s to use .

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
ll dp[10001][2][2][100] ;
ll n ; 
const ll mod = (ll)1e9 + 7 ;
ll solve(ll i, string& k ,bool tight , bool is_lz, ll d_sum , ll d) {
    if (i >= n) return  (d_sum % d == 0 && !is_lz) ;
    if (dp[i][tight][is_lz][d_sum] != -1LL) return dp[i][tight][is_lz][d_sum] ;
    ll lmt = tight ? k[i]-'0' : 9 ;
    
    ll cnt = 0LL ;
    for (ll digit = 0 ; digit <= lmt ; digit++) {
        cnt = (cnt + solve(i+1 , k , (tight&&(digit == lmt)) , (is_lz&&(digit==0)), (d_sum + digit)%d , d)) % mod ;
    }
    
    return dp[i][tight][is_lz][d_sum] = cnt ;
}
int main() {
    string k ;
    ll d ;
    cin >> k ; cin >> d ;
    n = k.length();
    memset(dp , -1LL, sizeof(dp)) ;
    
    cout << solve(0, k ,true,true,0LL, d) << endl ;
}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   10000 X 2 X 2 X 100    |  10000 digits, tight, is_leading_z, dSum all are to be explored atleast ones         |
| 🧠 SPACE |    10000 X 2 X 2 X 100      |     Dp table       |
