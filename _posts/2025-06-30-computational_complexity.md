# Computational Complexity

Computational complexity is a formal ([mathematical](math.md)) study of resource usage (usually time and memory) by [computers](computer.md) as they're solving various types of problems. For example when using computers to [sort](sorting.md) arrays of [numbers](number.md), computational complexity allows us to tell which [algorithm](algorithm.md) will be fastest as the size of the array grows, which one will demand the least amount of memory ([RAM](ram.md)) and even what's generally the fastest way in which this can be done. While time ("speed", number of steps) and memory (also *space*) are generally our primary resources of interest, other can be considered too, e.g. network or power usage. Complexity theory is invaluable and extremely important, it belongs among the most essential disciplines of [computer science](compsci.md); it is also immensely practically important as it helps us [optimize](optimization.md) our programs, it teaches us useful knowledge such as that we can trade time and space complexity (i.e. make program run faster on detriment of memory and vice versa) etc.

Primarily we have to distinguish between two basic types of complexity:

- **[algorithm](algorithm.md) complexity**: Complexity of a specific algorithm. For example [quick sort](quick_sort.md) and [bubble sort](bubble_sort.md) are both algorithms for sorting arrays but quick sort has better time complexity. (Sometimes we may extend this meaning and talk e.g. about memory complexity of a [data structure](data_structure.md) etc.)
- **problem complexity**: Complexity of the best algorithm that can solve particular problem; e.g. time complexity of sorting an array is given by time complexity of the algorithm that can sort arrays the fastest.

## Algorithm Complexity

Let us now focus on algorithm complexity, as problem complexity follows from it. OK, so **what really is the "algorithm complexity"?** Given resource *R* -- let's consider e.g. time, or the number of steps the algorithm needs to finish solving a problem -- let's say that complexity of a specific algorithm is a [function](function.md) *f(N)* where *N* is the size of input data (for example length of the array to be sorted), which returns the amount of the resource (here number of steps of the algorithm). However we may spot issues emerging here, most importantly that the number of steps may not only depend on the size of input data but also the data itself (e.g. with sorting it may take shorter time to sort and already sorted array) and on the computer we use (for example some computers may be unable to perform multiplication natively and will emulate it with SEVERAL additions, increasing the number of steps), and also the exact complexity function will be pretty messy (it likely won't be a nice smooth function but rather something that jumps around a bit). So this kind of [sucks](suck.md). We have to make several steps to get a nice, usable theory.

The **solution** to presented problem will be achieved in several steps.

FIRSTLY let's clarify with better precision what *f(N)* returns exactly -- when computing algorithm complexity we will always be interested in one of the following:

- **best case** scenario: Here we assume *f(N)* always returns the best possible value for given *N*, usually the lowest (i.e. least number of steps, least amount of memory etc.). So e.g. with array sorting for each array length we will assume the input array has such values that the given algorithm will achieve its best result (fastest sorting, best memory usage, ...). I.e. this is the **lower bound** for all possible values the function could give for given *N*.
- **average case** scenario: Here *f(N)* returns the average, i.e. taking all possible inputs for given input size *N*, we just average the performance of our algorithm and this is what the function tells us.
- **worst case** scenario: Here *f(N)* return the worst possible values for given *N*, i.e. the opposite of best case scenario. This is the **upper bound** for all possible value the function could give for given *N*.

This just deals with the fact that some algorithms may perform vastly different for different data -- imagine e.g. linear searching of a specific value in a list; if the searched value is always at the beginning, the algorithm always performs just one step, no matter how long the list is, on the other hand if the searched value is at the end, the number of steps will increase with the list size. So when analyzing an algorithm **we always specify which kind of case we are analyzing** (WATCH OUT: do not confuse these cases with differences between big O, big Omega and big Theta defined below). So let's say from now on we'll be implicitly examining worst case scenarios.

SECONDLY rather than being interested in PRECISE complexity functions we will rather focus on so called **asymptotic complexity** -- this kind of complexity is only concerned with how fast the resource usage generally GROWS as the size of input data approaches big values (infinity). So again, taking the example of array sorting, we don't really desire to know exactly how many steps we will need to sort any given array, but rather how the time needed to sort bigger and bigger arrays will grow. This is also aligned with practice in another way: we don't really care how fast our program will be for small amount of data, it doesn't matter if it takes 1 or 2 microseconds to sort a small array, but we want to know how our program will [scale](scalability.md) -- if we have 10 TB of data, will it take 10 minutes or half a year to sort? If this data doubles in size, will the sorting time also double or will it increase 1000 times? This kind of complexity also no longer depends on what machine we use, the rate of growth will be the same on fast and slow machine alike, so we can conveniently just consider some standardized computer such as [Turing machine](turing_machine.md) to mathematically study complexity of algorithms.

Rather than exact value of resource usage (such as exact number of steps or exact number of bytes in RAM) asymptotic complexity tells us a **[class](class.md)** into which our complexity falls. These classes are given by mathematical functions that grow as fast as our complexity function. So basically we get kind of "tiers", like *constant*, *linear*, *logarithmic*, *quadratic* etc., and our complexity simply falls under one of them. Some common complexity classes, from "best" to "worst", are following (note this isn't an exhaustive list):

- **constant**: Given by function *f(x) = 1* (i.e. complexity doesn't depend on input data size). Best.
- **[logarithmic](log.md)**: Given by function *f(x) = log(x)*. Note the base of logarithm doesn't matter.
- **linear**: Given by function *f(x) = x*.
- **linearithmic**: Given by function *f(x) = x * log(x)*.
- **quadratic**: Given by function *f(x) = x^2*.
- **cubic**: Given by function *f(x) = x^3*.
- **exponential**: Given by function *f(x) = n^x*. This is considered very bad, practically unusable for larger amounts of data.

Now we just put all the above together, introduce some formalization and notation that computer scientists use to express algorithm complexity, you will see it anywhere where this is discussed. There are the following:

- **big O (Omicron) notation**, written as *O(f(N))*: Says the algorithm complexity (for whatever we are measuring, i.e. time, space etc. and also the specific kind of case, i.e. worst/best/average) is asymptotically bounded from ABOVE by function *f(N)*, i.e. says the **upper bound** of complexity. This is probably the most common information regarding complexity you will encounter (we usually want this "pessimistic" view). More mathematically: complexity *f(x)* belongs to class *O(g(y))* if from some *N0* (we ignore some initial oscillations before this value) the function *f* always stays under function *g* multiplied by some positive constant *C*. Formally: *f(x) belongs to O(g(y)) => exists C > 0 and N0 > 0: for all n >= N0: 0 <= f(n) <= C * g(n)*.
- **big Omega notation**, written as *Omega(f(N))*: Says the algorithm complexity **lower bound** is given by function *f(N)*. Formally: *f(x) belongs to Omega(g(y)) => exists C > 0 and N0 > 0: for all n >= N0: 0 <= C * g(n) <= f(n)*.
- **big Theta notation**, written as *Theta(f(N))*: This just means the complexity is both *O(f(N))* and *Omega(f(N))*, i.e. the complexity is tightly bounded by given function.

Please note that big O/Omega/Theta are a different thing than analyzing best/worst/average case! We can compute big O, big Omega and big Theta for all best, worst and average case, getting 9 different "complexities".

Now notice (also check by the formal definitions) that we simply don't care about additive and multiplicative constants and we also don't care about some initial oscillations of the complexity function -- it doesn't matter if the complexity function is *f(x) = x* or *f(x) = 100000000 + 100000000 * x*, it still falls under linear complexity! If we have algorithm *A* and *B* and *A* has better complexity, *A* doesn't necessarily ALWAYS perform better, it's just that as we scale our data size to very high values, *A* will prevail in the end.

Another thing we have to clear up: **what does input size really mean?** I.e. what exactly is the *N* in *f(N)*? We've said that e.g. with array sorting we saw *N* as the length of the array to be sorted, but there are several things to additionally talk about. Firstly it usually doesn't matter if we measure the size of input in bits, bytes or number of items -- note that as we're now dealing with asymptotic complexity, i.e. only growth rate towards infinity, we'll get the same complexity class no matter the units (e.g. a linear growth will always be linear, no matter if our *x* axis measures meters or centimeters or light years). SECONDLY however it sometimes DOES matter how we define the input size, take e.g. an algorithm that takes a square image with resolution *R * R* on the input, iterates over all pixels and find the brightest one; now we can define the input size either as the total number of pixels of the image (i.e. *N = R * R*) OR the length of the image side (i.e. *N = R*) -- with the former definition we conclude the algorithm to have linear time complexity (for *N* input pixels the algorithm makes roughly *N* steps), with the latter definition we get QUADRATIC time complexity (for image with side length *N* the algorithm makes roughly *N * N* steps). What now, how to solve this? Well, this isn't such an issue -- we can define the input size however we want, we just have to **stay consistent** so that we are able to compare different algorithms (i.e. it holds that if algorithm *A* has better complexity than algorithm *B*, it will stay so under whatever definition of input size we set), AND when mentioning complexity of some algorithm we should mention how we define the input size so as to prevent confusion.

With memory complexity we face a similar issue -- we may define memory consumption either as an EXTRA memory or TOTAL memory that includes the memory storing the input data. For example with array sorting if an algorithm works [in situ](in_situ.md) (in place, needing no extra memory), considering the former we conclude memory complexity to be constant (extra memory needed doesn't depend on size of input array), considering the latter we conclude the memory complexity to be linear (total memory needed grows linearly with the size of input array). The same thing as above holds: whatever definition we choose, we should just mention which one we chose and stay consistent in using it.

## Problem Complexity

### [P vs NP]
The class P stands for polynomial and is defined as all problems that can be solved by an algorithm run on a deterministic Turing machine (a theoretical computer) with a polynomial time complexity.

The class NP stands for non-deterministic polynomial and is defined as all problems that can be solved by an algorithm run on a non-deterministic Turing machine with a polynomial time complexity. I.e. the definition is the same as for the P class with the difference that the Turing machine is non-deterministic -- such a machine is faster because it can make kind of "random correct guesses" that lead to the solution more quickly. Non-deterministic computers are only theoretical (at least for now), computers we have in real life cannot perform such randomly correct guesses. It is known that the solution to all NP problems can be verified in polynomial time even by a deterministic Turing machine, we just don't know if the solution can also be found this quickly.

As said, problem complexity is tied to algorithm complexity; a complexity of specific problem (e.g. sorting an array, factorization of a number, searching a sorted list etc.) is determined by the best possible [algorithm](algorithm.md) that solves the problem (best in terms of analyzed complexity). Traditionally we use [Turing machines](turing_machine.md) and [formal languages](formal_language.md) to analyze problem complexity. Here we'll stay a bit informal and only mention some ideas.

Similarly to algorithm complexity, with problems we again define **[classes](class.md)** that are only about "how quickly the resource usage grows as we increase input size". The main difference is we are examining problems, so the classes we get are classes of PROBLEMS (usually classes of formal languages, like e.g. in Chomsky's language hierarchy), not classes of functions (seen in algorithm complexity). Some common classes are:

- **DTime(f(x))**: Problems for whose solution a [DETERMINISTIC](determinism.md) Turing machine has an algorithm with time complexity *O(f(x))*.
- **NTime(f(x))**: Problems for whose solution a NON-DETERMINISTIC Turing machine has an algorithm with time complexity *O(f(x))*.
- **DSpace(f(x))**: Same as DTime but for space complexity.
- **NSpace(f(x))**: Same as NTime but for space complexity.
- **[P](p.md)**: Union of all classes *DTime(n^k)*, i.e. all problems that can be solved by a DETERMINISTIC Turing machine with [polynomial](polynomial.md) time complexity.
- **[NP](np.md)**: Union of all classes *NTime(n^k)*, i.e. the same as above but for NON-DETERMINISTIC Turing machine. It is currently not know [if classes P and NP are the same](p_vs_np.md), though it's believed to not be the case -- in fact this is probably the most famous yet unsolved problem of computer science.
- **EXP**: Union of all classes *DTime(2^n^k)*.
- ...

## Examples

Practically analyzing time complexity of algorithms mostly involves looking at the loops in our algorithm as these are what makes number of steps in algorithm variable. Linear sequences of instructions (such as initializations) don't interest us, no matter how long, as these have no effect on asymptotic complexity. But remember that looping may also be achieved with [recursion](recursion.md) etc., so just look carefully.

Let's consider the simple [bubble sort](bubble_sort.md) array sorting algorithm, with the simple optimization that ends as soon as the array is sorted; here it is written in [C](c.md):

```
void bubbleSort(int *array)
{
  for (int i = 0; i < N - 1; ++i)
  {
    int end = 1;

    for (int j = 0; j < N - 1 - i; ++j)
      if (a[j] > a[j + 1])
      {
        swap(&a[j],&a[j + 1]);
        end = 0;
      }

    if (end) // no swap happened => sorted, end
      break;
  }
}
```

The size of input data is the length of input array (`N`), for memory we consider only the extra memory used. Let's see about different complexities now:

- **asymptotic TIME complexity for WORST case**: Worst case happens when the optimizing condition (`if (end)`) never triggers and so both loops (outer and inner one) in our algorithm run all their iterations; the outer loop is performed approximately *N* times (actually *N - 1* times but remember that asymptotic complexity ignores -1 here as an additive constant) and for each of its iterations the inner loop runs approximately *N - i* times. So e.g. for *N = 5* we get approximately 5 + 4 + 3 + 2 + 1 steps, so for given *N* we basically have to sum up numbers from 1 to *N* -- there is a formula for computing such sum and that is *(N *(N + 1)) / 2 = N^2 / 2 + N / 2*. With asymptotic complexity we just take the biggest term and ignore any multiplication constant (division by two), so we just see *N^2* here and conclude that the time complexity of worst case for bubble sort is quadratic, i.e. *O(N^2)*. Notice that technically we can also say the complexity belongs to any "worse" class, e.g. *O(N^3)* (as *O(N^2)* is its subclass), which is technically true but doesn't tell us as much. So here it's better to further more precisely say the complexity of worst case also belongs to *Omega(N^2)* (the lower bound) and therefore (by belonging to both *O(N^2)* and *Omega(N^2)*) also belongs to *Theta(N^2)*, i.e. it "won't be slower BUT NOR faster than *N^2*".
- **asymptotic TIME complexity for BEST case**: Best case happens when the input array is already sorted -- here the algorithm enters the outer loop, then runs the inner loop -- approximately *N* iterations -- and then (since no swap happened) ends at the final condition. So the time complexity is linear -- we can say that the upper asymptotic bound on best case scenario is *O(N)*. Again we see the complexity is linearly bound from the bottom too so it's better to say the complexity of best case belongs to *Theta(N)*.
- **space (memory) complexity**: Bubble sort works in place and though it uses extra variables, the size of those variables doesn't depend on the size of input array, so (as we only count extra memory requirements) we can say memory complexity is constant, i.e. *O(1)*, and also *Theta(1)*.

