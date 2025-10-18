# K - Stones

- who wins is determined by the another one who can't win over a sum value after making a choice of x from array : a , if the nxt_player lose over sum-x then you can optimally win !
  
```cpp
#include <bits/stdc++.h>
#include <iomanip>
using namespace std;
#define ll long long
vector<ll> dp ;

ll solve( vector<ll>& a ,ll sum) {
    if (sum < a[0]) return 0 ;
    if (sum == a[0]) return 1 ;
    if (dp[sum] != -1) return  dp[sum] ;
    
    ll can_win = false ;
    for (ll x : a) {
        if (x == 0) continue ;
        if (x > sum) break ;
        if (solve( a , sum-x ) == 0) {
            can_win = true ;
            break ;
        }
    }
    return dp[sum] = can_win ;
}

int main() {
    ll n , k ; // ll is not needed for n <= 2999
    cin >> n >> k ;
    // TaroWin->1 , 0->Jiro
    dp.resize(k+1 ,-1) ;
    vector<ll> a(n) ;
    
    for (int i = 0; i < n ; i++ ) {
        cin >> a[i] ;
    }
    sort(a.begin() , a.end()) ;
    
    ll ans = solve(  a , k ) ;
    // print() ;
    
    if (ans) {
        cout << "First" <<endl ;
    }else {
        cout << "Second" <<endl ;
        
    }
}
```
# Tabulation Approach 
```cpp
#include <bits/stdc++.h>
#include <iomanip>
using namespace std;
#define ll long long

int main() {
    ll n , k ; // ll is not needed for n <= 2999
    cin >> n >> k ;
    // TaroWin->1 , 0->Jiro
    vector<bool> dp(k+1 , false) ;
    
    vector<ll> a(n) ;
    
    for (int i = 0; i < n ; i++ ) {
        cin >> a[i] ;
    }
    sort(a.begin() , a.end()) ;
    
    
    // print() ;
    
    for (int j = 1 ; j <= k ; j++ ) {
        
        for (int x : a) {
            if (x > j) break ;
            if (dp[j-x] == 0) { // prev player lose at j=sum
                dp[j] = true ;
                break ;
            }
        }
    }
    
    ll ans = dp[k] ;// ie Starting from Taro can he win otherwise Jiro 
    if (ans) {
        cout << "First" <<endl ;
    }else {
        cout << "Second" <<endl ;
        
    }
}
```
