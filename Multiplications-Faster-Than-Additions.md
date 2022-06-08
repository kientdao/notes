---
title: Multiplications and 2 additions are faster than 2 additions
date: 29-05-2022
private: false
---

I am reading Agner Fog's optimization manuals, and I came across this example:

```c
double data[LEN];

void compute()
{
    const double A = 1.1, B = 2.2, C = 3.3;

    int i;
    for(i=0; i<LEN; i++) {
        data[i] = A*i*i + B*i + C;
    }
}
```

Agner indicates that there's a way to optimize this code - by realizing that the loop can avoid using costly multiplications, and instead use the "deltas" that are applied per iteration.

I use a piece of paper to confirm the theory, first...

![](https://i.stack.imgur.com/wzzgt.png)

...and of course, he is right - in each loop iteration we can compute the new result based on the old one, by adding a "delta". This delta starts at value "A+B", and is then incremented by "2\*A" on each step.

So we update the code to look like this:

```c
void compute()
{
    const double A = 1.1, B = 2.2, C = 3.3;
    const double A2 = A+A;
    double Z = A+B;
    double Y = C;

    int i;
    for(i=0; i<LEN; i++) {
        data[i] = Y;
        Y += Z;
        Z += A2;
    }
}
```

In terms of operational complexity, the difference in these two versions of the function is indeed, striking. Multiplications have a reputation for being significantly slower in our CPUs, compared to additions. And we have replaced 3 multiplications and 2 additions... with just 2 additions!

So I go ahead and add a loop to execute `compute` a lot of times - and then keep the minimum time it took to execute:

```c
unsigned long long ts2ns(const struct timespec *ts)
{
    return ts->tv_sec * 1e9 + ts->tv_nsec;
}

int main(int argc, char *argv[])
{
    unsigned long long mini = 1e9;
    for (int i=0; i<1000; i++) {
        struct timespec t1, t2;
        clock_gettime(CLOCK_MONOTONIC_RAW, &t1);
        compute();
        clock_gettime(CLOCK_MONOTONIC_RAW, &t2);
        unsigned long long diff = ts2ns(&t2) - ts2ns(&t1);
        if (mini > diff) mini = diff;
    }
    printf("[-] Took: %lld ns.\n", mini);
}
```

I compile the two versions, run them... and see this:

```bash
# gcc -O3 -o 1 ./code1.c

# gcc -O3 -o 2 ./code2.c

# ./1
[-] Took: 405858 ns.

# ./2
[-] Took: 791652 ns.
```

Well, that's unexpected. Since we report the minimum time of execution, we are throwing away the "noise" caused by various parts of the OS. We also took care to run in a machine that does absolutely nothing. And the results are more or less repeatable - re-running the two binaries shows this is a consistent result:

```bash
# for i in {1..10} ; do ./1 ; done
[-] Took: 406886 ns.
[-] Took: 413798 ns.
[-] Took: 405856 ns.
[-] Took: 405848 ns.
[-] Took: 406839 ns.
[-] Took: 405841 ns.
[-] Took: 405853 ns.
[-] Took: 405844 ns.
[-] Took: 405837 ns.
[-] Took: 406854 ns.

# for i in {1..10} ; do ./2 ; done
[-] Took: 791797 ns.
[-] Took: 791643 ns.
[-] Took: 791640 ns.
[-] Took: 791636 ns.
[-] Took: 791631 ns.
[-] Took: 791642 ns.
[-] Took: 791642 ns.
[-] Took: 791640 ns.
[-] Took: 791647 ns.
[-] Took: 791639 ns.
```

The only thing to do next, is to see what kind of code the compiler created for each one of the two versions.

`objdump -d -S` shows that the first version of `compute` - the "dumb", yet somehow fast code - has a loop that looks like this:

[![objdump naive](https://i.stack.imgur.com/JbWNJ.png)](https://i.stack.imgur.com/JbWNJ.png)

What about the second, optimized version - that does just two additions?

[![objdump optimized](https://i.stack.imgur.com/HQwXx.png)](https://i.stack.imgur.com/HQwXx.png)

Now I don't know about you, but speaking for myself, I am... puzzled. The second version has approximately 4 times fewer instructions, with the two major ones being just SSE-based additions (`addsd`). The first version, not only has 4 times more instructions... it's also full (as expected) of multiplications (`mulpd`).

I confess I did not expect that result. Not because I am a fan of Agner (I am, but that's irrelevant).
