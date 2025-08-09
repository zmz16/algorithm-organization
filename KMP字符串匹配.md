# KMP算法

## 复杂度

时间复杂度: O(n + m)
空间复杂度: O(m)

## 代码实现

```cpp
// 获取前缀表/next数组
void getNext (int * next, const string & s) {
    // 初始化
    int j = 0;   // 前缀尾
    next[0] = 0;

    for (int i = 1; i < s.size(); i++) {
        // 处理前后缀不相同的情况
        while (j > 0 && s[i] != s[j]) {
            // 向前回退，直到找到相同的或者j为0
            j = next[j - 1];
        }

        // 处理前后缀相同的情况
        if (s[i] == s[j]) {
            j++;
        }
        next[i] = j;  // 将j（前缀的长度）赋给next[i]
    }
}

// KMP主算法
int kmpSearch (const string & text, const string & pattern) {
    // 模式串长度为0，直接返回
    if (pattern.size() == 0) {
        return 0;
    }

    // 获取前缀表
    int next[pattern.size()];
    getNext(next, pattern);

    int j = 0;   // 指向模式串
    for (int i = 0; i < text.size(); i++) {
        while (j > 0 && text[i] != pattern[j]) {
            j = next[j - 1];   // 不匹配时回退
        }

        if (text[i] == pattern[j]) {
            j++;
        }

        if (j == pattern.size()) {
            return i - pattern.size() + 1;   // 返回匹配起始位置
        }
    }

    return -1;   // 未找到
}
```
