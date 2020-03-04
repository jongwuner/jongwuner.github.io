---
layout:     post
title:      "Codeforces Ozon Tech Challenge 1305B - Kuroni and Simple Strings"
subtitle:   "어렵게 Construction 하지말자, Meet In The Middle, While문 기반 Constructure"
date:       2020-03-04 04:23:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Sort
  - Distinct Value
  - While loop
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75814003-58a6d580-5dd4-11ea-8d9f-ab879a491cc6.png)
![image](https://user-images.githubusercontent.com/16419202/75814025-63616a80-5dd4-11ea-8a93-12e0e0db4405.png)

<br><br><br><br><br>
## Approach
- Stack을 사용하는 구현 <- '('')' String의 전형적인 문제라고 떠올림.
- Queue를 사용하는 구현?
- 선형자료구조를 이용한(왼쪽에서부터의 '('개수, 오른쪽에서부터의 ')'개수) Construction
  - 문자열도 옮겨야 하는 문제발생. 
 
## Solution
- `Meet-In-The-Middle`이 제일 간단한 솔루션.
  - 가장 바깥의 왼쪽'(', 오른쪽')'부터 없애나가면 된다. 
- 결국 남는 것은 `)(` ,`))(((` 이런 식의 변형이기 때문에 마주보고 있는 `(` 와 `)`는 모두 없어진 결과이다. 
  
## Comment
- 물음에 답변해보자.
  - Stack이 아닌 이유는 무엇인가?
  - Queue가 아닌 이유는 무엇인가? (Queue로도 풀린다고 들었다. 어떤식으로 해야하는가?)
  - 선형자료구조 Construction은 왜 복잡한가? 
- `while문 설계` 가 까다로울때가 언제인가? 왜 부담을 느끼나?
  - `Queue`
  - `Stack` - 남는 값에 대한 처리
  - 선형자료구조, 인덱스 초과 런타임 오류방지 `while(ptr < N && .... )`
- String 빈자리 메꿀 때, s[i] = 0으로 하면 null이 되기때문에, s[i] = 1같은 방식이 좋다.  

## Code (Meet-In-The-Middle)
```cpp
#include<bits/stdc++.h>
using namespace std;
string S;
int ans = 0;
int N;
priority_queue<int> pq;
int main() {
	cin >> S;
	int Lptr = 0, Rptr = S.size() - 1;
	N = S.size();
	while (Lptr < Rptr) {
		while (Lptr < N && S[Lptr] != '(') Lptr++;
		while (0 <= Rptr && S[Rptr] != ')') Rptr--;
		
		if (!(Lptr < Rptr && S[Lptr] == '(' && S[Rptr] == ')')) break;
		ans++;
		pq.push(-(Lptr + 1)); 
		pq.push(-(Rptr + 1));
		Lptr++; Rptr--;
	}
	if (ans > 0) cout << "1\n" << 2 * ans << "\n";
	else cout << "0\n";
	while (!pq.empty()) {
		cout << -pq.top() << " ";
		pq.pop();
	}
	cout << "\n";
	return 0;
}
```
<br>
## Code (Queue)
N번 탐색에 대해서 Queue에 `(`와 `idx`를 같이 넣어준다. 이렇게 저장된 것을 다시 보면서
`)`일때 현재 idx가 queue에 들어가있는 `(`를 순차적으로 보면서 그것을 가리키고 있는 idx가 
현재 `)`을 보고 있는 idx보다는 항상 작아야 한다.  
<br>
```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define FOR(a,b,c) for(int a = (b); a <= (c); a++)
#define RFOR(a,b,c) for(int a = (b); a >= (c); a--)
#define all(x) (x).begin(), (x).end()
#define vi vector <int>
#define vvi vector <vi>
#define ll long long
#define vll vector <ll>
#define vvl vector <vll>
#define pii pair<int,int>
#define pll pair<ll,ll>
#define eb emplace_back
#define ep emplace
#define fs first
#define sd second
using namespace std;

int main() {
	FIO;
	//int t; cin >> t; while (t--) {
		string s;
		cin >> s;
		stack <int> st;
		queue <int> q;
		vi ans;
		int len = (int)s.size();
		FOR(i, 0, len - 1) {
			if (s[i] == '(') q.ep(i);
		}
		int cnt = len;
		RFOR(i, len - 1, 0) {
			if (s[i] == ')') {
				if (q.empty()) break;
				int a = q.front(); q.pop();
				if (a > i) break;
				
				ans.eb(i);
				ans.eb(a);
				cnt -= 2;
			}
		}
		sort(all(ans));
		if ((int)ans.size()) {
			cout << 1 << '\n';
			cout << (int)ans.size() << '\n';
			for (int i : ans) cout << i + 1 << ' ';
		}
		else cout << 0 << '\n';
	//}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1305B.cpp)
- [조세퍼스 문제 - while문 설계]()