---
layout: post
title:  "Code - Euler's Totient Function"
date:   2019-09-27 19:15:00 +0530
categories: algorithms
---
Euler's Totient Function of a number n, i.e phi(n), is the number of numbers lesser than n, that are co-prime to n.

## Computing phi(n)

{% highlight cpp %}
int phi(int n)
{
    int res=n;
    for(int i=2; i*i<=n; i++)
    {
        if(n%i==0)
        {
            while(n%i==0) n/=i;
            res-=res/i;
        }
    }
    if(n>1) res-=res/n;
    return res;
}
{% endhighlight %}

## Precomputing phi using Sieve

{% highlight cpp %}
int phi[N];

for(int i=1; i<N; i++) phi[i]=i;
for(int i=2; i<N; i++)
{
    if(phi[i]==i)
    {
        for(int j=i; j<N; j+=i) phi[j]-=phi[j]/i;
    }
}
{% endhighlight %}

## Precomputing phi using Linear Sieve

{% highlight cpp %}
bool is_composite[N];
vector<int> primes;
int phi[N];

phi[1]=1;
for(int i=2; i<N; i++)
{
    if(!is_composite[i])
    {
        primes.push_back(i);
        phi[i]=i-1;
    }
    for(int j=0; j<primes.size() && i*primes[j]<N; j++)
    {
        is_composite[i*primes[j]]=1;
        if(i%primes[j]==0)
        {
            phi[i*primes[j]]=phi[i]*primes[j];
            break;
        }
        else
        {
            phi[i*primes[j]]=phi[i]*phi[primes[j]];
        }
    }
}
{% endhighlight %}

### References

<https://cp-algorithms.com/algebra/phi-function.html>

<https://codeforces.com/blog/entry/54090>