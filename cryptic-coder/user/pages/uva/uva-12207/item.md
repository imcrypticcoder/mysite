---
title: 'UVA-12207 (Thats is your queue)'
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
/*
    Time :      0.039
    Rank :      150
*/

#include <set>
#include <map>
#include <list>
#include <cmath>
#include <ctime>
#include <queue>
#include <stack>
#include <cctype>
#include <cstdio>
#include <string>
#include <vector>
#include <cassert>
#include <cstdlib>
#include <cstring>
#include <sstream>
#include <iostream>
#include <algorithm>

using namespace std;

#define FOR(i, L, U) for(int i=(int)L; i<=(int)U; i++)
#define FORD(i, U, L) for(int i=(int)U; i>=(int)L; i--)

#define READ(x) freopen(x, "r", stdin)
#define WRITE(x) freopen(x, "w", stdout)

#define PQ priority_queue
#define PB push_back
#define SZ size()

#define EPS 1e-9
#define SQR(x) ((x)*(x))
#define INF 99999999

#define ALL_BITS ((1 << 31) - 1)
#define NEG_BITS(mask) (mask ^= ALL_BITS)
#define TEST_BIT(mask, i) (mask & (1 << i))
#define ON_BIT(mask, i) (mask |= (1 << i))
#define OFF_BIT(mask, i) (mask &= NEG_BITS(1 << i))

typedef long long LL;
typedef vector<int> VI;
typedef vector<vector<int> > VVI;
typedef vector<string> VS;
typedef vector<bool> VB;
typedef vector<char> VC;
typedef vector< vector<bool> > VVB;
typedef pair<int, int> PI;
typedef map<int, int> MII;
typedef map<char, int> MCI;
typedef map<string, int> MSI;

int GCD(int a,int b){   while(b)b^=a^=b^=a%=b;  return a;   }

#define WHITE 0
#define GRAY 1
#define BLACK 2

#define MAX_NODE 10001

int P, C;
list<int> l;


int main()
{
    READ("input.txt");
    //WRITE("output.txt");

    int i, j, k;
    int TC, tc;
    string line;
    char cmd;
    int cmdValue;

    tc = 1;
    while(cin >> P >> C) {
        getchar();
        if(P == 0 && C == 0) break;

        P = min (P, C);
        FOR(i, 1, P) l.push_back(i);

        cout << "Case " << tc++ << ":" << endl;
        FOR(i, 1, C) {
            getline(cin, line);
            stringstream ss(line);
            ss >> cmd;
            if(cmd == 'N') {
                cout << l.front() << "\n";
                l.push_back(l.front());
                l.pop_front();
            }
            else if(cmd == 'E') {
                ss >> cmdValue;
                l.remove(cmdValue);
                l.push_front(cmdValue);
            }
        }
        //cout << endl;
        l.clear();
    }

    return 0;
}
```