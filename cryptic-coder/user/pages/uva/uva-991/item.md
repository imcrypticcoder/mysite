---
title: 'UVA-991 (Safe Salutations)'
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

```java
/*
    Time :		0.212
    Rank :		1077
    Complexity:
*/

import java.math.BigInteger;
import java.util.Scanner;


public class Main {
	
	public static BigInteger[] cats = new BigInteger[11];
	
	public static void generateCatalans() {
		cats[0] = BigInteger.ONE;
		for(int i = 1; i <= 10; i++) {
			int n = i-1;
			cats[i] = BigInteger.valueOf(2 * (2*n + 1));
			cats[i] = cats[i].multiply(cats[n]);
			cats[i] = cats[i].divide(BigInteger.valueOf(n+2));
		}
	}
	
	public static void main(String args[]) {
		Scanner scr = new Scanner(System.in);
		
		generateCatalans();
		
		boolean isFirst = true;
		while(scr.hasNextInt()) {
			if( !isFirst ) System.out.println();
			isFirst = false;
			int n = scr.nextInt();
			System.out.println(cats[n].toString());
		}
	}
}
```