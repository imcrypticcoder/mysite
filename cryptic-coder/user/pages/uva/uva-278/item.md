---
title: 'UVA-278 (Chess)'
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
#include <cstdio>
#include <cmath>
#include <iostream>
#include <string.h>		// For memset function
#include <vector>
#include <list>
#include <stack>
#include <queue>
#include <string>
#include <algorithm>
#include <bitset>
#include <sstream>
#include <map>

using namespace std;

#define FOR( i, L, U ) for(int i=(int)(L) ; i<=(int)(U) ; i++ )
#define FORD( i, U, L ) for(int i=(int)(U) ; i>=(int)(L) ; i-- )
#define SQR(x) ((x)*(x))

#define INF 99999999
#define SZ size()
#define PB push_back
#define PF push_front

#define READ(filename)  freopen(filename, "r", stdin);
#define WRITE(filename)  freopen(filename, "w", stdout);

typedef long long LL;
typedef vector<int> VI;
typedef vector<vector<int> > VVI;
typedef vector<double> VD;
typedef vector<char> VC;
typedef vector<string> VS;
typedef pair<int, int> II;
typedef map<int, int> MII;
typedef map<char, int> MCI;
typedef map<string, int> MSI;
typedef map<string, char> MSC;
typedef map<string, string> MSS;

#define WHITE 0
#define GRAY 1
#define BLACK 2


int main()
{
//    READ("input.txt");
//    WRITE("output.txt");
    int i, j, k;
    int TC, tc;
    char ch;
    int m,n;
    cin >> TC;

    tc = 1;
    while(TC--) {
        cin >> ch >> m >> n;

        if(ch == 'r') {
            cout << min(m, n) << "\n";
        }
        else if(ch == 'Q') {
            cout << min(m, n) << "\n";
        }
        else if(ch == 'K') {
            int ans = (int)ceil((double)m/2) *  (int)ceil((double)n/2);
            cout << ans << "\n";
        }
        else if(ch == 'k') {
            if((m*n)%2 == 0)
                cout << (m*n)/2 << "\n";
            else cout << (m*n)/2 + 1 << "\n";
        }

    }

    return 0;
}
```