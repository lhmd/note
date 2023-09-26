---
title: code before this website
date: 2022-10-27 14:40:49
categories:
- 算法
tags: 
- code
- c++
---

# fds刷题记录

<!--more-->

### [PTA B 1003 我要通过!](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805323154440192)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int n,k,flag;
	char ch;
	scanf("%d",&n);
	getchar();

	while(n--) {
		int a[3]= {0};
		k=0;
		flag=1;
		while((ch=getchar())!='\n') {
			if(ch=='A')
				a[k]++;
			else if(ch=='P'&&k==0)
				k=1;
			else if(ch=='T'&&k==1)
				k=2;
			else
				flag=0;
		}
		if(flag&&k==2&&a[0]*a[1]==a[2]&&a[1]!=0)
			printf("YES\n");
		else
			printf("NO\n");
	}
	return 0;
}


```

### [初识dp：买卖股票最佳时机](https://leetcode.cn/leetbook/read/top-interview-questions-easy/x2zsx1/)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int size=prices.size();
        int dp[30005][2]={0},i;
        dp[0][1]=-prices[0];
        for(i=1; i<size; i++) {
            dp[i][0] = (dp[i-1][0]>dp[i-1][1]+prices[i])?dp[i-1][0]:dp[i-1][1]+prices[i];
            dp[i][1] = (dp[i-1][0]-prices[i]>dp[i-1][1])?dp[i-1][0]-prices[i]:dp[i-1][1];
        }
        return dp[size-1][0];
    }
};

/*此题利润累加法也可解<贪心算法>
public int maxProfit(int[] prices) {
    if (prices == null || prices.length < 2)
        return 0;
    int total = 0, index = 0, length = prices.length;
    while (index < length) {
        //如果股票下跌就一直找，直到找到股票开始上涨为止
        while (index < length - 1 && prices[index] >= prices[index + 1])
            index++;
        //股票上涨开始的值，也就是这段时间上涨的最小值
        int min = prices[index];
        //一直找到股票上涨的最大值为止
        while (index < length - 1 && prices[index] <= prices[index + 1])
            index++;
        //计算这段上涨时间的差值，然后累加
        total += prices[index++] - min;
    }
    return total;
}*/
```

### [异或运算的应用：查重](https://leetcode.cn/leetbook/read/top-interview-questions-easy/x21ib6/)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res=0;
        for(int i=0; i<nums.size(); i++) {
            res=res^nums[i];
        }
        return res;
    }
};
```

### [位运算的应用：判断数字是否重复](https://leetcode.cn/leetbook/read/top-interview-questions-easy/x2f9gg/)

```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int line[9] = {0};
        int column[9] = {0};
        int block[9] = {0};
        int shift = 0;
        for(int i = 0; i < 9; i++) {
            for(int j = 0; j <9; j++) {
                if(board[i][j] == '.') continue;
                shift = 1 << (board[i][j] - '0');
                int k = (i / 3) * 3 + j / 3;
                //如果对应的位置只要有一个大于0，说明有冲突，直接返回false
                if ((column[i] & shift) > 0 || (line[j] & shift) > 0 || (block[k] & shift) > 0)
                    return false;
                column[i] |= shift;
                line[j] |= shift;
                block[k] |= shift;
            }
        }
        return true;
    }
};
```

