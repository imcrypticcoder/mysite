---
title: 'UVA-11547 (Automatic Answer)'
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
#include <stdlib.h>

using namespace std;

int main()
{
    int TC,tc;
    int n, ans;

    cin >> TC;

    while(TC--) {
        cin >> n;
        ans = abs((n*63 + 7492)*5 - 498);
        ans = (ans%100)/10;
        cout << ans << endl;
    }

	return 0;
}
```