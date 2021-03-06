---
title: 'UVA-336 (A Node Too Far)'
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

#define EPS 1e-9
#define SQR(x) ((x)*(x))
#define INF 99999999
#define TO_DEG 57.29577951
#define PI 2*acos(0.0)

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
typedef pair<int, int> PII;
typedef map<int, int> MII;
typedef map<char, int> MCI;
typedef map<string, int> MSI;

int GCD(int a,int b){   while(b)b^=a^=b^=a%=b;  return a;   }

// UP, RIGHT, DOWN, LEFT, UPPER-RIGHT, LOWER-RIGHT, LOWER-LEFT, UPPER-LEFT
int dx[8] = {-1, 0, 1, 0, -1, 1,  1, -1};
int dy[8] = { 0, 1, 0,-1,  1, 1, -1, -1};

// Represents all moves of a knight in a chessboard
int dxKnightMove[8] = {-1, -2, -2, -1,  1,  2, 2, 1};
int dyKnightMove[8] = { 2,  1, -1, -2, -2, -1, 1, 2};

inline int src() { int ret; scanf("%d", &ret); return ret; }

#define WHITE 0
#define GRAY 1
#define BLACK 2

#define MAX_NODE 31

int NODES;
int EDGES;

int NC;
VVI G;
VC color;
MII nodeMap;
int TTL[MAX_NODE];

int BFS(int source, int ttl)
{
    int u, v;
    int nodesVisited;
    queue<int> Q;

    color = VC(NODES, WHITE);
    Q.push(source);
    color[source] = GRAY;
    TTL[source] = ttl;
    nodesVisited = 1;

    while( !Q.empty() ) {
        u = Q.front();  Q.pop();

        if(TTL[u] != 0) {
            FOR(i, 0, G[u].SZ-1) {
                v = G[u][i];
                if(color[v] == WHITE) {
                    nodesVisited++;
                    color[v] = GRAY;
                    Q.push(v);
                    TTL[v] = TTL[u] - 1;
                }
            }
        }
    }
    return nodesVisited;
}

int main()
{
    READ("input.txt");
    //    WRITE("output.txt");
    int i, j, k;
    int TC, tc;
    int u, v;
    int source, ttl;

    tc = 1;
    while(scanf("%d", &NC) == 1 && NC) {

        G = VVI(MAX_NODE);
        int nodeLabel = -1;
        FOR(i, 1, NC) {
            scanf("%d %d", &u, &v);
            if(nodeMap.find(u) == nodeMap.end()) nodeMap[u] = (++nodeLabel);
            if(nodeMap.find(v) == nodeMap.end()) nodeMap[v] = (++nodeLabel);
            G[nodeMap[u]].PB(nodeMap[v]);
            G[nodeMap[v]].PB(nodeMap[u]);
        }
        NODES = nodeMap.size();

        while(cin >> source >> ttl) {
            if(source == 0 && ttl == 0) break;
            int visited = BFS(nodeMap[source], ttl);
            printf("Case %d: %d nodes not reachable from node %d with TTL = %d.\n", tc++, NODES-visited, source, ttl);
        }

        G.clear();
        nodeMap.clear();
    }


    return 0;
}
```