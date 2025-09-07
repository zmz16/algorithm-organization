# Prim 算法

```cpp
#include<iostream>
#include<vector>
#include <climits>

using namespace std;
int main() {
    int v, e;
    int x, y, k;
    cin >> v >> e;
    vector<vector<int>> grid(v + 1, vector<int>(v + 1, 10001));
    while (e--) {
        cin >> x >> y >> k;
        grid[x][y] = k;
        grid[y][x] = k;
    }

    vector<int> minDist(v + 1, 10001);
    vector<bool> isInTree(v + 1, false);

    //加上初始化
    vector<int> parent(v + 1, -1);

    for (int i = 1; i < v; i++) {
        int cur = -1;
        int minVal = INT_MAX;
        for (int j = 1; j <= v; j++) {
            if (!isInTree[j] &&  minDist[j] < minVal) {
                minVal = minDist[j];
                cur = j;
            }
        }

        isInTree[cur] = true;
        for (int j = 1; j <= v; j++) {
            if (!isInTree[j] && grid[cur][j] < minDist[j]) {
                minDist[j] = grid[cur][j];

                parent[j] = cur; // 记录边
            }
        }
    }
    // 输出 最小生成树边的链接情况
    for (int i = 1; i <= v; i++) {
        cout << i << "->" << parent[i] << endl;
    }
}
```
