---
title: 'UVA-10147 (Highways)'
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
    Time :
    Rank :
*/

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

//---------------------------- GLOBAL VARIABLES ----------------------------

struct POINT {
   double x, y;
};

double sqr_dist(POINT a, POINT b)
{
   return sqrt(SQR(a.x - b.x) + SQR(a.y - b.y));
}

vector<POINT> pnts;
int existEdge;

//---------------------------- KRUSKAL ALGO START --------------------------
typedef struct {
    int u, v;
    double w;
} EDGE;

int NODES, EDGES;
vector<EDGE> edges;
vector<EDGE> spanEdge;
vector<EDGE> newEdge;
double minSpanCost;

// -------------------- Disjoint Set Structure --------------------------------------
int set[10001];
void InitSet(int N)     {   FOR(i, 1, N)    set[i] = i;     }
int FindSet(int u)      {   return set[u] == u ? u : (set[u] = FindSet(set[u]));    }
void Union(int u, int v){   set[FindSet(u)] = FindSet(v); }
// ----------------------------------------------------------------------------------

int compEdge(EDGE a, EDGE b)
{
    return a.w < b.w;
}

void Kruscal()
{
	int p, q;

   minSpanCost = 0.0;

	for(int i=0; i < EDGES; i++) {
		p = FindSet(edges[i].u);
		q = FindSet(edges[i].v);
		if(p != q) {
			spanEdge.push_back(edges[i]);
			newEdge.PB(edges[i]);
			Union(p, q);
			minSpanCost += edges[i].w;
			if(spanEdge.size() == NODES - 1) break;
		}
	}
}
//---------------------------- KRUSKAL ALGO END --------------------------

int main()
{
    READ("input.txt");
//    WRITE("output.txt");
   int i, j, k;
   int TC, tc;
   POINT p;
   EDGE e;
   int u, v;

   cin >> TC;

   FOR(tc, 1, TC) {
      if(tc > 1) cout << endl;

      cin >> NODES;
      pnts = vector<POINT>(NODES + 1);
      FOR(i, 1, NODES) {
         cin >> p.x >> p.y;
         pnts[i] = p;
      }
      FOR(i, 1, NODES) FOR(j, i+1, NODES) {
         e.u = i;
         e.v = j;
         e.w = sqr_dist(pnts[i], pnts[j]);
         edges.PB(e);
      }
      EDGES = edges.SZ;

      InitSet(NODES + 1);
      cin >> existEdge;
      FOR(i, 1, existEdge) {
         cin >> e.u >> e.v;
         int p = FindSet(e.u);
         int q = FindSet(e.v);
         if(p != q) {
            Union(e.u, e.v);
            spanEdge.PB(e);
         }
      }
      if(spanEdge.SZ == NODES-1) {
         cout << "No new highways need\n";
      }
      else {
         sort(edges.begin(), edges.end(), compEdge);
         Kruscal();

         FOR(i, 0, newEdge.SZ-1) {
            cout << newEdge[i].u << " " << newEdge[i].v << endl;
         }
      }


      edges.clear();
      spanEdge.clear();
      pnts.clear();
      newEdge.clear();
   }

   return 0;
}
```