# Prime Number

Prime number (or just *prime*) is a whole positive numbers only divisible by 1 and itself, except for the number 1. I.e. prime numbers are 2, 3, 5, 7, 11, 13, 17 etc. Non-prime numbers are called *composite numbers*. The simplicity of definition might bring about an impression that prime numbers are something plain, akin to odd numbers for example, but this couldn't be further from the truth: you'll learn from any mathematician that primes are not only vitally important to their field, but immensely interesting, complex and even mysterious for their intricate properties and relatively "random" distribution among other numbers, they have for millennia fascinated mathematics because they are so simple and complex at the same time, and they're still not fully understood to this day. Nowadays they are studied by so called number theory, a subfield of mathematics Primes are also of practical use, for example in asymmetric cryptography Primes can be seen as the opposite of highly composate numbers (also antiprimes, numbers that have more divisors than any lower number). Numbers of comparable status and similarly mysterious properties to prime numbers are for example perfect numbers, whose importance is however a bit diminished by current lack of practical use.

```
.##.#.#...#.#...#.#...#.....#.#.....#...#.#...#.....#.....#.#.....#...
```

*Prime number positions up to 70.*

The largest known prime number as of 2022 is 2^82589933 - 1 (it is so called Mersenne prime, i.e. a prime of form 2^N - 1).

Every natural number greater than 1 has a unique **prime factorization**, i.e. a [set](set.md) of prime numbers whose product it is. For example 75 is a product of three primes: 3 * 5 * 5. This is called the *fundamental theorem of arithmetic*. Naturally, each prime has a factorization consisting of a single number -- itself -- while factorizations of non-primes consist of at least two primes. To mathematicians prime numbers are what chemical elements are to chemists -- a kind of basic building blocks.

**Why is 1 not a prime?** Out of convenience -- if 1 was a prime, the fundamental theorem of arithmetic would not hold because 75's factorization could be 3 * 5 * 5 but also 1 * 3 * 5 * 5, 1 * 1 * 3 * 5 * 5 etc. It also makes sense under some different definitions -- imagine for example we create a [tree](tree.md) of numbers, assign each number *N* a parent number *M* which is the maximum of all *N*'s divisors that we check from 1 (including) to *N* (excluding); in this tree prime numbers are all numbers in depth 1, i.e. those that are direct children of 1, but 1 itself is not at this level, it's at the root, having no parent (as it would be its own parent), so by this definition 1 is also not a prime.

The unique factorization can also nicely be used to encode [multisets](multiset.md) as numbers. We can assign each prime number its sequential number (2 is 0, 3 is 1, 5 is 2, 7 is 3 etc.), then any number encodes a set of numbers (i.e. just their presence, without specifying their order) in its factorization. E.g. 75 = 3 * 5 * 5 encodes a multiset {1, 2, 2}. This can be exploited in cool ways in some [cyphers](cypher.md) etc.

```
       _ _   _   _       _   _       _   _       _           _   _
     1 2 3 4 5 6 7 8 9 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 3 3 3 3 3
                       0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4
     ____________________________________________________________________
  1 |<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
  2 |  <>||<>||<>||<>  <>||<>||<>  <>||<>||<>  <>||<>  <>  <>||<>||<>  <>
  3 |    <>  ||<>||  <>  ||<>||  <>  ||<>||  <>  ||<>    <>  ||<>||  <>
  4 |      <>||  ||<>    ||<>||    <>||  ||<>    ||<>      <>||  ||<>
  5 |        <>  ||    <>||  ||  <>  ||  ||<>    ||  <>      ||<>||
  6 |          <>||      ||<>||      ||<>||      ||          ||  ||
  7 |            <>      ||  ||<>    ||  ||  <>  ||          ||  ||
  8 |              <>    ||  ||    <>||  ||      ||<>        ||  ||
  9 |                <>  ||  ||      ||<>||      ||      <>  ||  ||
 10 |                  <>||  ||      ||  ||<>    ||          ||<>||
 11 |                    <>  ||      ||  ||    <>||          ||  ||  <>
 12 |                      <>||      ||  ||      ||<>        ||  ||
 13 |                        <>      ||  ||      ||    <>    ||  ||
 14 |                          <>    ||  ||      ||        <>||  ||
 15 |                            <>  ||  ||      ||          ||<>||
 16 |                              <>||  ||      ||          ||  ||<>
 17 |                                <>  ||      ||          ||  ||    <>
 18 |                                  <>||      ||          ||  ||
 19 |                                    <>      ||          ||  ||
 20 |                                      <>    ||          ||  ||
```

*Divisibility of numbers on top by numbers on the left -- we can see prime numbers as the ones avoided by all divisors (except 1 and self), i.e. the ones for which we can draw a continuous straight vertical line between the top line (divisibility by 1) and the diagonal (divisibility by self).*

When in 1974 the Arecibo radio message was sent to space to carry a message for [aliens](alien.md), the resolution of the bitmap image it carried was chosen to be 73 x 23 pixels -- two primes. This was cleverly done so that when aliens receive the 1679 sequential values, there are only two possible ways to interpret them as a 2D bitmap image: 23 x 73 (incorrect) and 73 x 23 (correct). This increased the probability of correct interpretation against the case of sending an arbitrary resolution image.

**There are infinitely many prime numbers**. The proof is quite elementary (shown below), however it's pretty fascinating that it has still not been proven whether there are infinitely many **[twin primes](twin_prime.md) (primes that differ by 2)**, which, despite its similarity to the original problem, shows to be an incomparably more difficult question to answer. The notion of "twin prime" can be extended to prime triplets (3 primes with gaps 2 and 4, in either order), prime cousins (primes spaced by 4), sexy primes (primes spaced by 6) and eventually generalized to so called prime *k-tuples*: tuples describing prime patterns with offsets, e.g. [0, 2, 6] specifies one possible form of a prime triplet etc. -- you may even hear the term *prime constellation* (it's almost as if prime numbers are like stars in the sky, together forming certain shapes). Another simple but unproven conjecture related to prime numbers is [Goldbach's conjecture](goldbachs_conjecture.md) stating that every even number greater than 2 can be written as a sum of two primes.

Euklid's [proof](proof.md) shows there are infinitely many primes, it is conducted by contradiction and goes as follows: suppose there are finitely many primes *p1*, *p2*, ... *pn*. Now let's consider a number *s* = *p1* * *p2* * ... * *pn* + 1. This means *s* - 1 is divisible by each prime *p1*, *p2*, ... *pn*, but *s* itself is not divisible by any of them (as it is just 1 greater than *s* and multiples of some number *q* greater than 1 have to be spaced by *q*, i.e. more than 1). If *s* isn't divisible by any of the considered primes, it itself has to be a prime. However that is in contradiction with the original assumption that *p1*, *p2*, ... *pn* are all existing primes. Therefore a finite list of primes cannot exist, there have to be infinitely many of them.

**Distribution and occurrence of primes**: the occurrence of primes seems kind of """[random](random.md)""" (a bit like digits of [decimal](decimal.md) representation of [pi](pi.md)), without a simple pattern. Obviously *randomness* here doesn't stand for "true randomness", as primality of any number is perfectly [determined](determinism.md) and [decidable](decidability.md), but as far as our knowledge reaches, there aren't simple ways to perfectly predict for example occurrence of primes with a simple, fast to compute formula, i.e. *randomness* rather stands for [chaos](chaos.md). Hints of patterns appear such as the [Ulam spiral](ulam_spiral.md) -- upon plotting natural numbers in a square spiral and marking the primes, we visually perceive a dimly appearing 45 degree diagonals as well as horizontal and vertical lines. Furthermore the **density of primes decreases** the further away we go from 0. The *prime number theorem* states that a number randomly chosen between 0 and *N* (for large *N*) has approximately 1/log(N) [probability](probability.md) of being a prime. **Prime counting function** is a [function](function.md) which for *N* tells the number of primes smaller or equal to *N*. While there are 25 primes under 100 (25%), there are 9592 under 100000 (~9.5%) and only 50847534 under 1000000000 (~5%).

```
         ,   ,     ,    ',  '    ,'  , ,  '
      ',',          '      ,  ' ',  ' ',
,,   ,   ,'     '     ',   ,'      ,'  ,      ' '
 ,     ,    ', ,  '  ,' ', ,'             '  ,', ,
      '     ',',     ,   ,          ',    ',
,    , ,               ,'  ,' '   ',   , ,      '
     ,',   ,',  '  , ,     ,' '  ,  '        ,
, ',  ' ',     ,   ,'      ,    ',  '     ' '    ,
  ',', , ,'   '  ,     ,'   ' '  ,',' ',     , ,
            '     '   ' ', ,     ,   ,  ', ,  ', ,
      '   '   '   ' '   ', ,   ,'   ' '         ',
  ' ',  ', , , ,', ,',',   ,' ' '  ,  ' ' '  , ,
     ,             ,   ,',;,', , ,   , ,',     ,
  ' '       '       ',' ',
,,' '  ,  '  ,' ',  ','   ',  ' ', ,'  ,' '   ',
     , ,         , ,  '  ,   ,   ,'      , ,  '
      ' ',    ',  '  ,   , ,  '       '     '
,,       , , , ,    ' '  ,',    ',  '  , ,'  ,','
 ,     ,   ,',  '  ,     ,  ',',           ,     ,
  ',    ' '       ', ,   , ,'       ',    ',
,   ',       , ,'   ',    '     '      ,  ' '
 ,    '   '       '           '   ',    ',   ,
   ,  '   ' '   '    ,'    ,   , ,'             ',
 ,'     ',     ,   ,',   ,  '    ,     ,    '   '
     ,            ',     ,   , ,     ,   ,'   ',
```

*Ulam spiral: the center of the image is the number 1, the number line continues counter clockwise, each point represents a prime.*

Here are prime numbers under 1000: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701, 709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997.

Here are twin prime numbers under 1000: 3, 5, 7, 11, 13, 17, 19, 29, 31, 41, 43, 59, 61, 71, 73, 101, 103, 107, 109, 137, 139, 149, 151, 179, 181, 191, 193, 197, 199, 227, 229, 239, 241, 269, 271, 281, 283, 311, 313, 347, 349, 419, 421, 431, 433, 461, 463, 521, 523, 569, 571, 599, 601, 617, 619, 641, 643, 659, 661, 809, 811, 821, 823, 827, 829, 857, 859, 881, 883.

```
                                      ______/
                                     /     /
                        _____ ______/_    /
                 ____  /     X     /__\  /
          ___   /    \/__   / \   /__  \/
         /   \ /     /\  \ /   \ /   \ /\
--2--3--/--5--X--7--/--\--X--11-X--13-X--\--
   \__\/ \  \/ \__\/ \  \/ \__\/ \  \/ \__\/
       \__\_/\  \ /\  \ /\__\_/\  \ /\  \ /\
           \__\__X  \  X  \  X  \  X__\__X
               \__\__\/ \  \/ \  \/ \  \/ \
                   \__\__\_/\  \ /\  \ /\  \
```

There also exists a term **pseudoprime** -- it stands for a number which is not actually a prime but appears so because it passes some quick primality tests.

**Higher order primes**, also **superprimes** or prime-indexed primes, are primes occupying prime numberth position within prime numbers, i.e. one of first higher order primes is for example number 5 because it is the 3rd prime and 3 itself is a prime. 5 is also one of second order higher primer numbers because it is 2nd first higher order prime number and 2 is a prime number. Etc. So we may generalize this concept to a prime number order *R(x)*, which says the highest order that number *x* achieves in this sense, with *R(x) = 0* meaning *x* is not prime at all. One of very high superprimes is for example number 174440041 (lowest number with *R(x) = 12*). Prime orders for numbers up to 1000 are (leaving out the ones with order 0):

2: 1, 3: 2, 5: 3, 7: 1, 11: 4, 13: 1, 17: 2, 19: 1, 23: 1, 29: 1, 31: 5, 37: 1, 41: 2, 43: 1, 47: 1, 53: 1, 59: 3, 61: 1, 67: 2, 71: 1, 73: 1, 79: 1, 83: 2, 89: 1, 97: 1, 101: 1, 103: 1, 107: 1, 109: 2, 113: 1, 127: 6, 131: 1, 137: 1, 139: 1, 149: 1, 151: 1, 157: 2, 163: 1, 167: 1, 173: 1, 179: 3, 181: 1, 191: 2, 193: 1, 197: 1, 199: 1, 211: 2, 223: 1, 227: 1, 229: 1, 233: 1, 239: 1, 241: 2, 251: 1, 257: 1, 263: 1, 269: 1, 271: 1, 277: 4, 281: 1, 283: 2, 293: 1, 307: 1, 311: 1, 313: 1, 317: 1, 331: 3, 337: 1, 347: 1, 349: 1, 353: 2, 359: 1, 367: 2, 373: 1, 379: 1, 383: 1, 389: 1, 397: 1, 401: 2, 409: 1, 419: 1, 421: 1, 431: 3,
433: 1, 439: 1, 443: 1, 449: 1, 457: 1, 461: 2, 463: 1, 467: 1, 479: 1, 487: 1, 491: 1, 499: 1, 503: 1, 509: 2, 521: 1, 523: 1, 541: 1, 547: 2, 557: 1, 563: 2, 569: 1, 571: 1, 577: 1, 587: 2, 593: 1, 599: 3, 601: 1, 607: 1, 613: 1, 617: 2, 619: 1, 631: 1, 641: 1, 643: 1, 647: 1, 653: 1, 659: 1, 661: 1, 673: 1, 677: 1, 683: 1, 691: 1, 701: 1, 709: 7, 719: 1, 727: 1, 733: 1, 739:
2, 743: 1, 751: 1, 757: 1, 761: 1, 769: 1, 773: 2, 787: 1, 797: 2, 809: 1, 811: 1, 821: 1, 823: 1, 827: 1, 829: 1, 839: 1, 853: 1, 857: 1, 859: 2, 863: 1, 877: 2, 881: 1, 883: 1, 887: 1, 907: 1, 911: 1, 919: 3, 929: 1, 937: 1, 941: 1, 947: 1, 953: 1, 967: 2, 971: 1, 977: 1, 983: 1, 991: 2, 997: 1.

Out of autistic curiosity we may turn this into a "race" for firsts, i.e. look for first prime of order *N* for each *N*. Here we go: 2 (order 1), 3 (2), 5 (3), 11 (4), 31 (5), 127 (6), 709 (7), 5381 (8), 52711 (9), 648391 (10), 9737333 (11), ...

**Prime gaps**: statistically gaps between consecutive primes increase. The size of the gaps themselves make another number sequence that starts like this 1, 2, 2, 4, 2, 4, 2, 4, 6, 2, 6, 4, 2, 4, 6, 6, 2, 6, 4, 2, 6, 4, 6, 8, 4, 2, 4, 2, 4, 14, 4, 6, 2, 10, 2, 6, 6, 4, 6, 6, 2, 10, 2, 4, 2, 12, 12, 4, 2, 4, 6, 2, 10, 6, 6, 6, 2, 6, 4, 2, 10, 14, 4, 2, 4, 14, 6, 10, 2, 4, 6, 8, 6, 6, 4, 6, 8, 4, 8, 10.

**[Fun](fun.md) with primes**: thanks to their interesting, mysterious and [random](randomness.md) nature, primes can be played around with -- of course, you can examine them mathematically, which is always fun, but you can also play sort of [games](game.md) with them. For example the prime race: you make two teams of primes, one that gives 1 modulo 4, the other one that gives 3; then you go prime by prime and add points to each team depending on which one the prime falls in; the interesting thing is that team 3 is almost always in lead just by a tiny amount (this is known as Chebyshev bias, only after 2946 primes team 1 gets in the lead for a while, then at 50378 etc.). Similar thing can be done by evaluating the Mobius function: set total sum to 0, then go number by number and if it only has unique prime factors, add 1 if the number of those factors is even, otherwise subtract 1 -- see how the function behaves. Of course you can go crazy, make primes paint pictures or compose [music](music.md) -- people also like to do this with digits of numbers, e.g. those of [pi](pi.md) or [e](e.md).

**Can we generalize/modify the concept of prime numbers?** Yeah, sure, why not? The ways are many, we'll rather run into the issue of analysis paralysis -- choosing the interesting generalization of out of the many possible ways. Some possible generalizations include:

- **pseudoprimes**: the above mentioned, i.e. non-primes passing many prime tests.
- **almost primes**: a number is *n*-almost prime if it has *n* prime factors, so 1-almost primes are just regular primes (they have 1 prime divisor -- themselves) but then there are 2 almost primes like 9 or 15 that are kind of closer to being primes than let's say 5-almost-primes such as 48 or 80. We take the idea of numbers having either none (primes) or some (non-primes) divisors and generalized it by says a number is more prime like if it has fewer divisors.
- Another idea hinted on above: make a [tree](tree.md) of numbers with 1 as its root, assign each number a parent that's its greatest divisor (excluding the number itself); in this tree 1 is above prime numbers, prime numbers are on level 1, second level may be seen as the "next best thing" to primes (4, 6, 9, 10, 15, ...), third level the next (8, 12, 18, 27) and so on, i.e. we define the "primeness" as the depth in this tree, the number of times we have to replace the number with its greatest divisor before we get to 1.
- **[complex](complex_number.md) (Gaussian) primes**: This is not a strict generalization because we remove some primes by were primes before, but we may define prime numbers also within complex integers. Here we get primes to be 3, 7, 11, 19, 23 etc.
- Similarly we may try to play on this observation: a non-prime is a number that is divisible by something, i.e. there is some number that when dividing the original number gives remainder after division zero; primes are those for which no number gives remainder zero, but some primes might be considered "weaker" by giving very low or very high remainder such as 1, i.e. being "not quite but almost" divisible by something (of course we have to somehow account for the fact that low divisors can only ever give low remainders) -- ideal prime would have remainders after division near the half of the dividing number (it would dodge multiples of other numbers with some margin), which we can formalize and define kind of "prime strength".
- TODO: generalization to non integers? haven't found anything
- ...

## Algorithms

**Primality test**: testing whether a number is a prime is quite easy and not computationally difficult (unlike factoring the number). A [naive](naive.md) algorithm is called *trial division* and it tests whether any number from 2 up to the tested number divides the tested number (if so, then the number is not a prime, otherwise it is). This can be [optimized](optimization.md) by only testing numbers up to the [square root](sqrt.md) (including) of the tested number (if there is a factor greater than the square root, there is also another smaller than it which would already have been tested). A further simple optimization is to to test division by 2, 3 and then only numbers of the form 6q +- 1 (other forms are divisible by either 2 or 3, e.g 6q + 4 is always divisible by 2). Further optimizations exist and for maximum speed a [look up table](lut.md) may be used for smaller primes. A simple [C](c.md) function for primality test may look e.g. like this:

```c
int isPrime(int n) {
  if (n < 4)
    return n > 1;

  if (n % 2 == 0 || n % 3 == 0)
    return 0;

  int test = 6;

  while (test <= n / 2){ // replace n / 2 by sqrt(n) if available {
    if (n % (test + 1) == 0 || n % (test - 1) == 0){
      return 0;
    }

    test += 6;

    }

  }

  return 1;
}
```


[Sieve of Eratosthenes](sieve_of_eratosthenes.md) is a simple algorithm to find prime numbers up to a certain bound *N*. The idea of it is following: create a list of numbers up to *N* and then iteratively mark multiples of whole numbers as non-primes. At the end all remaining (non-marked) numbers are primes. If we need to find all primes under *N*, this algorithm is more efficient than testing each number under *N* for primality separately (we're making use of a kind of [dynamic programming](dynamic_programming.md) approach).

**[Prime factorization](factorization.md)**: We can factor a number by repeatedly [brute force](brute_force.md) checking its divisibility by individual primes and there exist many algorithms applying various optimizations (wheel factorization, Dixon's factorization, ...), however for factoring large (hundreds of bits) primes there exists no known efficient algorithm, i.e. one that would run in [polynomial time](polynomial_time.md), and it is believed no such algorithm exists (see [P vs NP](p_vs_np.md)). Many cryptographic algorithms, e.g. [RSA](rsa.md), rely on factorization being inefficient. For [quantum](quantum.md) computers a polynomial ("fast") algorithm exists, it's called [Shor's algorithm](shors_algorithm.md).

