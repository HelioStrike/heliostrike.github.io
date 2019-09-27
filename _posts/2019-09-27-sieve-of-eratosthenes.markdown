---
layout: post
title:  "Code - Sieve of Eratosthenes"
date:   2019-09-27 19:00:00 +0530
categories: algorithms
---
Sieve of Eratosthenes is an efficient way to precompute primes up to a number.

## Classic Sieve

{% highlight cpp %}
bool is_composite[N];
vector<int> primes;

for(int i=2; i<N; i++)
{
    if(!is_composite[i])
    {
        primes.push_back(i);
        // mark multiples of i as composite
        for(int j=2*i; j<N; j+=i) is_composite[j] = 1;
    }
}
{% endhighlight %}

## Linear Sieve

{% highlight cpp %}
int lp[N]; // stores the lowest prime factor of numbers
vector<int> primes;

for(int i=2; i<N; i++)
{
    if(!lp[i]) 
    {
        // If a number doesn't have a lower prime factor, it is prime
        lp[i]=i;
        primes.push_back(i);
    }
    for(int j=0; j<primes.size() && primes[j]<=lp[i] && i*primes[j]<N; j++) lp[i*primes[j]] = primes[j];
}
{% endhighlight %}

### References

<https://codeforces.com/blog/entry/54090>

<https://cp-algorithms.com/algebra/prime-sieve-linear.html>