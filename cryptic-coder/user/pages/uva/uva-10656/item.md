---
title: 'UVA-10656 (Maximum Sum 2)'
published: true
date: '00:05 11/02/2016'
taxonomy:
    category:
        - blog
    tag:
        - uva
body_classes: 'header-lite fullwidth blogstyling'
---

Here is full code:

===

```cpp
#include <iostream>

using namespace std;

int set[1001];


int main()
{
	int N, i, j;
	bool flag;
	
	while(cin >> N && N != 0) {
		flag = 0;
		for(i=1; i<=N; i++) {
			cin >> set[i];
			if(set[i] != 0) flag = 1;
		}
		
		for(j=1;j<N ;j++)
			if(set[j]) { cout << set[j];	break; }
									

		for(i=j+1;i<=N; i++) 
			if(set[i])  cout << " " << set[i];

		if(flag==0) cout << "0";
		cout << "\n";
	}
return 0;
}
```