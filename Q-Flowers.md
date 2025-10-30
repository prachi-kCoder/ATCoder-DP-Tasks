# Q-Flowers

- Brute force O(N x N) gives tle so its the time to use Fenwick Tree allowing for faster range sums and faster updates to get the incresing seq with max sum .
- `i & -i`: Use to remove the rightmost set bit
- While query we make take the max of sum of beauties of any increasing range as fenwick tree is made by considering h[i]-1 so all val < ht[i] are considered so every range has sum of beauties of incresing seq get the max of them
- Query : Take query of set bits
- Updates : Update by adding right set bits as increasingly {Having all num in the range}


```cpp
#include <bits/stdc++.h>

using namespace std;


int main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
	int n; cin>>n;
	vector<int> a, b, c; 
	for(int i = 0; i < n; i++){
		int A, B, C; cin>>A>>B>>C;
		a.push_back(A); 
		b.push_back(B); 
		c.push_back(C); 
	}
	vector<vector<int>> dp(n, vector<int>(3, 0)); 
	dp[0][0] = a[0]; 
	dp[0][1] = b[0]; 
	dp[0][2] = c[0]; 
	for(int i = 1; i < n; i++){
		dp[i][0] = max(dp[i - 1][1], dp[i - 1][2]) + a[i]; 
		dp[i][1] = max(dp[i - 1][0], dp[i - 1][2]) + b[i];
		dp[i][2] = max(dp[i - 1][1], dp[i - 1][0]) + c[i]; 
	}
	int ans = max(max(dp[n - 1][0], dp[n - 1][1]), dp[n - 1][2]);
	cout<<ans<<'\n'; 
}
    
```
