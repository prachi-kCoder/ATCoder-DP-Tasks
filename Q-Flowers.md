# Q-Flowers

- Brute force O(N x N) gives tle so its the time to use Fenwick Tree allowing for faster range sums and faster updates to get the incresing seq with max sum .
- `i & -i`: Use to remove the rightmost set bit
- While query we make take the max of sum of beauties of any increasing range as fenwick tree is made by considering h[i]-1 so all val < ht[i] are considered so every range has sum of beauties of incresing seq get the max of them
- Query : Take query of set bits
- Updates : Update by adding right set bits as increasingly {Having all num in the range}


```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll N = (ll)(2e5 + 5) ;
ll bit[N] ;
void update(int i, ll val) {
    for (; i < N; i += i & -i)
        bit[i] = max(bit[i], val);
}

ll query(int i) {
    ll res = 0;
    for (; i > 0; i -= i & -i)
        res = max(res, bit[i]);
    return res;
}
int main() {
	int n;
    cin >> n;
    vector<int> h(n);
    vector<ll> a(n);
    for (int i = 0; i < n; i++) cin >> h[i];
    for (int i = 0; i < n; i++) cin >> a[i];
    ll ans = 0;
    for (int i = 0; i < n; i++) {
        ll best = query(h[i] - 1);
        ll curr = best + a[i];
        update(h[i], curr);
        ans = max(ans, curr);
    }
    cout << ans << endl;

}    
```
