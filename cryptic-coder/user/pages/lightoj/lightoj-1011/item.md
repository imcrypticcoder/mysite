---
title: 'LIGHTOJ-1011 (Marriage Ceremonies)'
published: true
date: '00:05 11/02/2016'
taxonomy:
    category:
        - blog
    tag:
        - light-oj
body_classes: 'header-lite fullwidth blogstyling'
---

Here is full code:

===

```cpp
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
#define ff first
#define ss second

#define EPS 1e-9
#define SQR(x) ((x)*(x))
#define INF 99999999

#define ALL_BITS ((1 << 31) - 1)
#define NEG_BITS(mask) (mask ^ ALL_BITS)
#define TEST_BIT(mask, i) (mask & (1 << i))
#define ON_BIT(mask, i) (mask | (1 << i))
#define OFF_BIT(mask, i) (mask & NEG_BITS(1 << i))

typedef long long LL;
typedef vector<char> VC;
typedef vector<vector<char> > VVC;
typedef vector<int> VI;
typedef vector<vector<int> > VVI;
typedef vector<string> VS;
typedef vector<bool> VB;
typedef vector< vector<bool> > VVB;
typedef pair<int, int> PII;
typedef map<int, int> MII;
typedef map<char, int> MCI;
typedef map<string, int> MSI;

int GCD(int a,int b){   while(b)b^=a^=b^=a%=b;  return a;   }

#define WHITE 0
#define GRAY 1
#define BLACK 2

int dx[] = {1, -1, 0, 0};
int dy[] = {0, 0, -1, 1};

inline int src() { int ret; scanf("%d", &ret); return ret; }

#define MAXN 17

int N;
int p[MAXN][MAXN];
int memo[1 << 16];

int matching(int mask, int row)
{
   if(row > N-1) return 0;
   if(memo[mask] != -1) return memo[mask];

   int ret = -1;

   FOR(i, 0, N-1)
      if(!TEST_BIT(mask, i)) {
         ret = max(ret, p[row][i] + matching(ON_BIT(mask, i), row+1));
      }

   return memo[mask] = ret;
}

int main()
{
    READ("input.txt");
//    WRITE("output.txt");
   int i, j, k;
   int TC, tc;

   cin >> TC;

   FOR(tc, 1, TC) {
      cin >> N;

      FOR(i, 0, N-1) FOR(j, 0, N-1)
         scanf("%d", &p[i][j]);

      memset(memo, -1, sizeof memo);
      printf("Case %d: %d\n", tc, matching(0, 0));
   }
   return 0;
}
```