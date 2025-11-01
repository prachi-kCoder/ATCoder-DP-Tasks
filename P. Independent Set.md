# P. Independent Set


```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7 ;
vector<vector<ll>> adj ;
vector<vector<ll>> dp ;
void dfs(ll u, vector<bool>& vis) {
    vis[u] = true ;
    
    dp[u][0] = dp[u][1] = 1 ;
    for(ll v : adj[u]) {
        if (!vis[v]) {
            dfs(v , vis) ;
            dp[u][0] *= (dp[v][0] + dp[v][1]) ;
            dp[u][0] %= mod ;
            dp[u][1] *= (dp[v][0]) ;
            dp[u][1] %= mod ;
        }
    }
}
int main() {
    ll n ;
    cin >> n ;
    adj.resize(n) ;
    dp.resize(n, vector<ll>(2, 0LL)) ;
    
    for (ll i = 0 ; i < n-1 ; i++) {
        ll u , v ;
        cin >> u >> v ;
        u-- , v-- ;
        adj[u].push_back(v) ;
        adj[v].push_back(u) ;
    }
    vector<bool> vis(n , false);
    dfs(0, vis) ;
    
    cout << ( dp[0][0] + dp[0][1] )%mod << endl ;
    return 0;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)     | All nodes are being visited at most ones at computing dp[i][0] i being White Node , dp[i][1] i begin Black node |
| 🧠 SPACE |    O(V + E) + O(N x 2)      | Dp table  + O(V + E) Adj list of graph            |
