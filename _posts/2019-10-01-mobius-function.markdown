---
layout: post
title:  "Code - Mobius Function"
date:   2019-10-01 12:30:00 +0530
categories: algorithms
---
Mobius Function of n is,

1, if n is a square-free number with even number of prime factors

-1, if n is a square-free number with odd number of prime factors

0, if n has a squared prime factor

## Computing mobius(n) using Linear Sieve

{% highlight cpp %}
int lpf[N];
int mob[N];
vector<int> primes;

mob[1]=1;
for(int i=2;i<N;i++)
{
    if(lpf[i]==0)
    {
        mob[i]=-1; lpf[i]=i;
        primes.push_back(i);
    }
    for(int j=0; j<primes.size() && i*primes[j]<N && primes[j]<=lpf[i];j++)
    {
        int nxt=i*primes[j];
        if(primes[j]==lpf[i])
        {
            mob[nxt]=0;
            lpf[nxt]=primes[j];
        }
        else
        {
            mob[nxt]=mob[i]*-1;
            lpf[nxt]=primes[j];
        }
    }
}
{% endhighlight %}

### References

<https://en.wikipedia.org/wiki/M%C3%B6bius_function>

<https://codeforces.com/blog/entry/54090>

<https://cp-algorithms.com/algebra/prime-sieve-linear.html>