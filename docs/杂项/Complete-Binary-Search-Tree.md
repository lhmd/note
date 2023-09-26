---
title: Complete Binary Search Tree
date: 2022-10-30 23:19:35
tags:
- 递归
- c++
categories:
- 算法
---

### [Complete Binary Search Tree](https://pintia.cn/problem-sets/1582215244956827648/exam/problems/1582215245019742217)

<!--more-->

​	本题采取先排序，再将这个问题转换为中序遍历填数字的问题，简化了代码。

```c
#include<stdio.h>
int a[10005], b[10005], n, flag;
void sort(){
	int i, j;
	for(i = 0; i < n - 1; i++) {
		int cnt = 0;
		for(j = 0; j < n - 1 - i; j++) {
			if(a[j] > a[j+1]) {
				int temp = a[j];
				a[j] = a[j+1];
				a[j+1] = temp;
				cnt = 1;
			}
		}
		if(!cnt)break;
	}
}
void inorder(int i) {
	if(2*i <= n)inorder(2*i);
	b[i] = a[flag];
	flag ++;
	if(2*i+1 <= n)inorder(2*i+1);
}
int main() {
	int i;
	scanf("%d", &n);
	for(i = 0; i < n; i++) {
		scanf("%d", &a[i]); 
	}
	sort();
	inorder(1);
	for(i = 1; i < n; i++) {
		printf("%d ", b[i]);
	}
    printf("%d", b[i]);
}
```

