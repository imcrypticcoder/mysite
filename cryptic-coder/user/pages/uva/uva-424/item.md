---
title: 'UVA-424 (Integer Inquiry)'
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
#include <cstring>
#include <cmath>

using namespace std;

#define maxlength 500
#define max(a,b) ((a) > (b) ? (a) : (b))

class Mbigint {
public:
	int length;
	int digit[maxlength];

	Mbigint(int=0);
	~Mbigint() {}
	void checklength();
	void operator=(long M);
	void operator=(char *str);
	void operator=(Mbigint M);
	Mbigint operator+(Mbigint M);
	Mbigint operator*(Mbigint M);
	Mbigint operator*(int M);
	Mbigint operator/(int M);
	Mbigint operator%(int M);

	bool operator<(Mbigint M);
	bool operator<=(Mbigint M);
	bool operator>(Mbigint M);
	bool operator>=(Mbigint M);
	bool operator==(Mbigint M);
	bool operator!=(Mbigint M);

	void operator+=(Mbigint M);

};

void show(Mbigint M);

Mbigint::Mbigint(int v)
{
	(*this)=v;
	//this->checklength();
}

void Mbigint::checklength()
{
 for(;length>0 && digit[length]==0;length--);
}

void Mbigint::operator=(long M)
{
	memset(digit,0, maxlength*sizeof(int));

	for(length=0; M!=0; M /= 10000)
		digit[++length] = M % 10000;
	checklength();
}

void Mbigint::operator=(char *str)
{
	int L = strlen(str), temp = 0, i,j, k;
	length = (L + 3)/4;

	for(i=0;i < L%4; i++)
		temp = temp * 10 + (str[i] - '0');

	digit[length] = temp;

	j=0;
	if(L%4==0) k = length;
	else k = length - 1;
	temp = 0;
	for(i=L%4; i<L; i++) {
		temp = temp * 10 + (str[i] - '0');
		j++;
		if(j%4==0) {
			digit[k--] = temp;
			temp =0;
			j=0;
		}
	}
}

void Mbigint::operator=(Mbigint M)
{
	length = M.length;
	memcpy(digit, M.digit, maxlength*sizeof(int));
	this->checklength();

}
Mbigint Mbigint::operator+(Mbigint M)
{
	if (M.length==0)
		return (*this);
	if (length==0)
		return M;

	Mbigint T;
		T.length=max(length,M.length)+1;
		for (int i=1,temp=0;i<=T.length;i++)
			T.digit[i]=(temp=(temp/10000+digit[i]+M.digit[i]))%10000;
		T.checklength();
		return T;
}

Mbigint Mbigint::operator*(int M)
{
	Mbigint T;
	int temp=0, i;

	T.length = length+2;
	
	for(i=1; i<=T.length; i++)
		T.digit[i] = (temp=(temp/10000+digit[i]*M)) % 10000;
	T.checklength();
	return T;
}

Mbigint Mbigint::operator*(Mbigint M)
{
	int number, i, j, k, temp;
	Mbigint T;

	T.length = length + M.length;

	for(i=1; i<=length; i++) {
		number = digit[i];
		temp  = 0;

		for(j=1; j<=M.length; j++)
			T.digit[i+j-1] += number*M.digit[j];
		if(!(i%10) || i == length)
			for(j=1; j<=T.length; j++)
				T.digit[j] = (temp=(temp/10000)+T.digit[j]) % 10000;
	}
	T.checklength();
	return T;
}


Mbigint Mbigint::operator/(int M)
{
	int temp = 0, i;
	Mbigint T;

	T.length = length;
	for(i=T.length; i>=1; i--)
		T.digit[i] = (temp=(temp%M*10000 + digit[i])) / M;
	T.checklength();
	return T;
}

Mbigint Mbigint::operator%(int M)
{
	int temp=0;
	for(int i = length; i>=1; i--)
		temp = (temp*10000 + digit[i])% M;

	return temp;
}

// COMPARISON FUNCTION START HERE --------------------------------------------

bool Mbigint::operator<(Mbigint M)
{
	if(length != M.length)
		return length < M.length;
	for(int i = length; i>=1; i--)
		if(digit[i] != M.digit[i])
			return digit[i]<M.digit[i];
	return false;
}

bool Mbigint::operator<=(Mbigint M)	{		return !(M<(*this));	}
bool Mbigint::operator>(Mbigint M)		{		return M<(*this);			}
bool Mbigint::operator>=(Mbigint M)	{		return !((*this)<M);	}

bool Mbigint::operator==(Mbigint M)	
{		
	return (!((*this) < M) && (!((*this) > M)));	
}

bool Mbigint::operator!=(Mbigint M)	
{		
	return (((*this) < M) || ((*this) > M));	
}


void Mbigint::operator+=(Mbigint M)
{
	(*this) = (*this)+M;
}

// PRESENTATION FUNCTION START HERE --------------------------------------------

void show(Mbigint M)
{
	printf("%d", M.digit[M.length]);

	for(int i=M.length-1; i>=1; i--)
		printf("%04d", M.digit[i]);
}

int main()
{

	char str[1000];
	Mbigint result, temp;

	while(scanf("%s", str)) {
		if(str[0] == '0')
			break;
		temp = str;
		result += temp;
	}
	show(result);
	printf("\n");
	
return 0;
}
```