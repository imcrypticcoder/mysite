---
title: 'UVA-591 (Box of bricks)'
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

int main()
{
	int n, i, t_case;
	int h[51], sum, avg, moves;

	for(t_case =1; cin >> n && n != 0; t_case++) {
		sum = moves = 0;

		for(i=0; i<n; i++) {
			cin >> h[i];
			sum += h[i];
		}

		avg = sum / n;
		for(i=0; i<n; i++)
			if(h[i] > avg)
				moves += h[i] - avg;


		cout << "Set #" << t_case << "\n";
		cout << "The minimum number of moves is " << moves << ".\n\n";

	}

return 0;
}
```