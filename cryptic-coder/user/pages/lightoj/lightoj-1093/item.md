---
title: 'LIGHTOJ-1093 (Ghajini)'
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

#define ff first
#define ss second
#define PQ priority_queue
#define PB push_back
#define SZ size()

#define EPS 		1e-9
#define SQR(x) 		((x)*(x))
#define INF 		2000000000
#define TO_DEG 		57.29577951
#define PI 			2*acos(0.0)

#define ALL_BITS					((1 << 31) - 1)
#define NEG_BITS(mask)				(mask ^= ALL_BITS)
#define TEST_BIT(mask, i)			(mask & (1 << i))
#define ON_BIT(mask, i)				(mask |= (1 << i))
#define OFF_BIT(mask, i)			(mask &= NEG_BITS(1 << i))
#define IS_POWER_TWO(x)				(x && !(x & (x-1)))
#define OFF_RIGHTMOST_SET_BIT(x)	(x & (x-1))

typedef long long LL;
typedef unsigned long long ULL;
typedef pair<int, int> PII;
typedef pair<double, double> PDD;
typedef vector<bool> VB;
typedef vector<int> VI;
typedef vector<double> VD;
typedef vector<char> VC;
typedef vector<string> VS;
typedef map<int, int> MII;
typedef map<char, int> MCI;
typedef map<string, int> MSI;
typedef vector<vector<bool> > VVB;
typedef vector<vector<int> > VVI;
typedef vector<vector<double> > VVD;
typedef vector<vector<PII> > VVPII;

int GCD(int a, int b) { while (b)b ^= a ^= b ^= a %= b;  return a; }

// UP, RIGHT, DOWN, LEFT, UPPER-RIGHT, LOWER-RIGHT, LOWER-LEFT, UPPER-LEFT
int dx[8] = { -1, 0, 1, 0, -1, 1,  1, -1 };
int dy[8] = { 0, 1, 0,-1,  1, 1, -1, -1 };

// Represents all moves of a knight in a chessboard
int dxKnightMove[8] = { -1, -2, -2, -1,  1,  2, 2, 1 };
int dyKnightMove[8] = { 2,  1, -1, -2, -2, -1, 1, 2 };

inline int src() { int ret; scanf("%d", &ret); return ret; }

#define WHITE 0
#define GRAY 1
#define BLACK 2

#define MAX 100007

int N, d;
int A[MAX];
int st1[3 * MAX];
int st2[3 * MAX];

inline int left(int p) { return p << 1; }
inline int right(int p) { return (p << 1) + 1; }

void build(int p, int L, int R) {
	if (L == R) {
		st1[p] = st2[p] = L;
		return;
	}

	build(left(p), L, (L + R) / 2);
	build(right(p), (L + R) / 2 + 1, R);

	int p1 = st1[left(p)], p2 = st1[right(p)];
	st1[p] = (A[p1] <= A[p2]) ? p1 : p2;

	p1 = st2[left(p)], p2 = st2[right(p)];
	st2[p] = (A[p1] >= A[p2]) ? p1 : p2;
}

int minQuery(int p, int L, int R, int i, int j) {
	if (i > R || j < L) return -1;
	if (L >= i && R <= j) return st1[p];

	int p1 = minQuery(left(p), L, (L + R) / 2, i, j);
	int p2 = minQuery(right(p), (L + R) / 2 + 1, R, i, j);

	if (p1 == -1) return p2;
	if (p2 == -1) return p1;

	return (A[p1] <= A[p2]) ? p1 : p2;
}

int maxQuery(int p, int L, int R, int i, int j) {
	if (i > R || j < L) return -1;
	if (L >= i && R <= j) return st2[p];

	int p1 = maxQuery(left(p), L, (L + R) / 2, i, j);
	int p2 = maxQuery(right(p), (L + R) / 2 + 1, R, i, j);

	if (p1 == -1) return p2;
	if (p2 == -1) return p1;

	return (A[p1] >= A[p2]) ? p1 : p2;
}

int maxDiff() {
	int ret = 0;
	FOR(i, 0, N - d) {
		int a1 = A[maxQuery(1, 0, N-1, i, i + d - 1)];
		int a2 = A[minQuery(1, 0, N - 1, i, i + d - 1)];
		if (a1 - a2 > ret) ret = a1 - a2;
	}
	return ret;
}

int main()
{
	READ("input.txt");
	//WRITE("output.txt");
	int i, j, k;
	int TC, tc;
	double cl = clock();

	TC = src();

	FOR(tc, 1, TC) {
		scanf("%d %d", &N, &d);
		FOR(i, 0, N - 1) scanf("%d", &A[i]);

		build(1, 0, N-1);

		printf("Case %d: %d\n", tc, maxDiff());
	}

	cl = clock() - cl;
	fprintf(stderr, "Total Execution Time = %lf seconds\n", cl / CLOCKS_PER_SEC);

	return 0;
}
```