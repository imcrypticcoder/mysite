---
title: 'UVA-941 (Permutation)'
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

#define FOR( i, L, U ) for(int i=(int)L ; i<=(int)U ; i++ )
#define FORD( i, U, L ) for(int i=(int)U ; i>=(int)L ; i-- )
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

#define WHITE 0
#define GRAY 1
#define BLACK 2

vector<LL> f;
VC v;

LL fact(LL num)
{
    LL ret = 1;
    FOR(i, 2, num)
        ret *= i;
    return ret;
}

void InitFact()
{
    f = vector<LL>(20);
    LL fact = 1;
    f[1] = fact;

    FOR(i, 2, 19) {
        fact *= i;
        f[i] = fact;
    }
}

VI getPattren(LL num)
{
    VI ret;
    int p;
    LL temp = num;

    FORD(i, 19, 1) {
        p = 0;
        while(temp - f[i] >= 0) {
            temp = temp - f[i];
            p++;
        }
        ret.PB(p);
    }

    return ret;
}

int main()
{
 //   READ("input.txt");
 //   WRITE("output.txt");
    int i, j, k;
    int TC, tc;
    string str;
    LL N;

    InitFact();

//   FOR(i, 1, 19)
 //       cout << f[i] << "\n";

    cin >> TC;

    FOR(tc, 1, TC) {
        cin >> str;
        sort(str.begin(), str.end());

        FOR(i, 0, str.SZ-1)
            v.PB(str[i]);

        cin >> N;

        VI pattern = getPattren(N);

    //    FOR(i, 0, pattern.SZ-1)
    //        cout << pattern[i] << " ";

        FOR(i, 19-str.SZ+1, pattern.SZ-1) {
            cout << v[pattern[i]];
            v.erase(v.begin() + pattern[i]);
        }
        cout << v[0];
        v.erase(v.begin() + 0);
        cout << "\n";
    }

	return 0;
}
```