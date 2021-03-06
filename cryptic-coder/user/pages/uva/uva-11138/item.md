---
title: 'UVA-11138 (nuts and bolts)'
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
#define NEG_BITS(mask) (mask ^= ALL_BITS)
#define TEST_BIT(mask, i) (mask & (1 << i))
#define ON_BIT(mask, i) (mask |= (1 << i))
#define OFF_BIT(mask, i) (mask &= NEG_BITS(1 << i))

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


int M, N;         // Set A contains M nodes, Set B contains N nodes;
VVI G, res;       // Graph and Residual
int source, sink; // Source and Sink
VI parent;
int maxflow;

int bfs(int s, int t)
{
   queue<int> Q;

   Q.push(s);
   Q.push(INF);

   while( !Q.empty() ) {
      int u = Q.front();      Q.pop();
      int flow = Q.front();   Q.pop();
      if(u == t) {
         while(!Q.empty()) Q.pop();
         return flow;
      }
      FOR(i, 0, G[u].SZ-1) {
         int v = G[u][i];
         if(res[u][v] > 0 && parent[v] == -1) {
            Q.push(v);
            Q.push(min(flow, res[u][v]));
            parent[v] = u;
         }
      }
   }
   return 0;
}

void augmentPath(int s, int t, int flow)
{
   int cur = t;
   while(cur != s) {
      res[parent[cur]][cur] -= flow;
      res[cur][parent[cur]] += flow;
      cur = parent[cur];
   }
}

int maxFlow()
{
   parent = VI(M+N+2, -1);

   int flow;

   maxflow = 0;
   while((flow = bfs(source, sink)) != 0) {
      maxflow += flow;
      augmentPath(source, sink, flow);
      parent = VI(M+N+2, -1);
   }
   return maxflow;
}

int main()
{
    READ("input.txt");
//    WRITE("output.txt");
   int i, j, k;
   int TC, tc;
   int temp;

   scanf("%d", &TC);

   FOR(tc, 1, TC) {
      scanf("%d %d", &M, &N);

      G = VVI(M+N+2);
      res = VVI(M+N+2, VI(M+N+2));

      FOR(i, 1, M)
         FOR(j, 1, N) {
            res[i][M+j] = src();
            if(res[i][M+j] == 1) {
               G[i].PB(M+j);        //    Linking nodes
               G[M+j].PB(i);        //    Linking nodes
            }
         }

      // 0 is the super Source
      source = 0;
      // Connecting Super Source
      FOR(i, 1, M) {
         res[0][i] = 1;
         G[0].PB(i);
         G[i].PB(0);
      }

      // M+N+1 is the super sink
      sink = M+N+1;
      // Connecting Super Sink
      FOR(i, 1, N) {
         res[M + i][M + N + 1] = 1;
         G[M + i].PB(M + N + 1);
         G[M + N + 1].PB(M + i);
      }

      maxFlow();
      printf("Case %d: a maximum of %d nuts and bolts can be fitted together\n", tc, maxflow);
   }

   return 0;
}
```