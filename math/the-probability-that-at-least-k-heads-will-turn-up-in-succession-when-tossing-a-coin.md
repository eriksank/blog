#The probability that at least k heads will turn up in succession when tossing a coin

##Tossing a coin twice

When tossing a coin twice (n=2), the probability to toss two heads in a row is:

	P(2) = 1/2 * 1/2 = 1/4:

If we look at all 4 possibilities, it becomes clear why this must be so:

	(0) 0 0
	(1) 0 1
	(2) 1 0
	(3) 1 1  --> only this sequence satisfies the condition
		     while there are 4 possible sequences

##Tossing a coin three times

We can derive the probability of tossing two heads in a row for n=3 from the result for n=2 as following. Head is represented by a '1' and tail is represented by a '0':

	(0) 0 0 0
	(1) 0 0 1
	(2) 0 1 0
	(3) 0 1 1 

Half of the cases will be prefixed with a '0'. No new sequences of '1 1' could therefore be introduced at the beginning of the binary number representing the end of the tossing series. Therefore, P1(3) = 1/2 * P(2).

	(4) 1 0 0
	(5) 1 0 1

The other half of the cases will be prefixed with a '1'. Half of the remaining cases will themselves start with a '0'. No new sequences of '1 1' could therefore be introduced at the beginning of the binary number. The likelihood that these cases contain an occurrence of '1 1' depends on the P(1). Therefore, P2(3) = 1/4 * P(1) = 0.

	(6) 1 1 0
	(7) 1 1 1 

For another quarter of the cases, P3(3) = 1/4, because the sequence always starts with '1 1'. Therefore, the complete solution for P(3) is:

	P(3) = P1(3) + P2(3) + P3(3) = 1/2 * P(2) + 1/4 
	     = 1/2 * 1/4 + 1/4 = 3/8.

##Tossing a coin four times

For P(4) we can apply the same logic. There are 2^4 = 16 possible cases, with the first 8 starting with a '0', the next 4 starting with '1 0' and the last 4 starting with '1 1':

	(0) 0 0 0 0
	(1) 0 0 0 1
	(2) 0 0 1 0
	(3) 0 0 1 1 +
	(4) 0 1 0 0
	(5) 0 1 0 1
	(6) 0 1 1 0 +
	(7) 0 1 1 1 +

P1(4) = 1/2*P(3)

	(8)   1 0 0 0
	(9)   1 0 0 1
	(10)  1 0 1 0
	(11)  1 0 1 1 +

P2(4) = 1/4* P(2) = 1/4 * 1/4 = 1/16

	(12) 1 1 0 0 +
	(13) 1 1 0 1 +
	(14) 1 1 1 0 +
	(15) 1 1 1 1 +

P3(4) = 1/4

Therefore, P(4) = 1/2*P(3) +  1/4* P(2) + 1/4.

##General solution for tossing a coin n times and two consecutive heads

The general solution is therefore: 

	P(n) = 1/2*P(n-1) + 1/4*P(n-2) + 1/4﻿

Examples:

	P(4) = 1/2 * P(3) +1/4 * P(2) +1/4= 8/16. 

	P(5) = 1/2 * P(4) + 1/4 * P(3) + 1/4 = 19/32

	P(6) = 1/2 * P(5) + 1/4 * P(4) + 1/4 
	     = 1/2*19/32+1/4*8/16+1/4 = 19/64+8/64+16/64 = 43/64. ﻿

	P(7) = 1/2 * P(6) + 1/4 * P(5) + 1/4 
 	     = 1/2*43/64+1/4*19/32+1/4
	     = 43/128+19/128+32/128 = 94/128

General solution for k consecutive heads

If we toss n times, the population of possible outcomes can be represented by the set of number:

	{ 0, 1, 2, 3, ..., (2^n)-1 }

Each number, written in binary form, represents a possible sequence of tosses, with '1' representing a head and '0' representing a tail.

The function hasHeadSequence(i,k) returns true if the number i has k consecutive heads. From there, we can define:

	P(n,k) = sum(hasHeadSequence(i,k))/2^n

            i=0..(2^n)-1

With P(n,k) being the probability that we will have k consecutive heads when the coin n times.

The function prefix(b,i) prefixes the number i with the boolean digit '1' or '0', with:

	prefix('0',i) = i
	prefix('1',i) = 2^(n+1)+i

We can now define the function Px:

	Px(b,n,k) = sum(hasHeadSequence(prefix(b,i),k))/2^n
                i=0..(2^n)-1

The main property of the function Px is:

	Px('',n,k) = 1/2*Px('0',n-1,k) + 1/2*Px('1',n-1,k)

The properties of the function Px lend themselves to deriving P(n,k) in recursive terms. For k=2:

	P(n,2) = Px('',n,2)
	= 1/2*Px('0',n-1,2) + 1/2*Px('1',n-1,2)
	= 1/2*Px('0',n-1,2) + 1/4*Px('10',n-2,2) +  1/4*Px('11',n-2,2)

	= 1/2*P(n-1,2) + 1/4*P(n-2,2) + 1/4

For k=3, that is, 3 consecutive heads:

	P(n,3) = Px('',n,3)
	= 1/2*Px('0',n-1,3) + 1/2*Px('1',n-1,3)
	= 1/2*Px('0',n-1,3) + 1/4*Px('10',n-2,3) +  1/4*Px('11',n-2,3)
	= 1/2*Px('0',n-1,3) + 1/4*Px('10',n-2,3) +  
	    1/8*Px('110',n-3,3) +  1/8*Px('111',n-3,3)
	= 1/2*P(n-1,3) + 1/4*P(n-2,3) + 1/8*P(n-3,3) + 1/8

for k=4, that is, 4 consecutive heads:

	P(n,4) = Px('',n,4)
	= 1/2*Px('0',n-1,4) + 1/2*Px('1',n-1,4)
	= 1/2*Px('0',n-1,4) + 1/4*Px('10',n-2,4) +  1/4*Px('11',n-2,4)
	= 1/2*Px('0',n-1,4) + 1/4*Px('10',n-2,4) 
	   +  1/8*Px('110',n-3,4) +  1/8*Px('111',n-3,4)
	= 1/2*Px('0',n-1,4) + 1/4*Px('10',n-2,4) +  1/8*Px('110',n-3,4) 
	   +  1/16*Px('1110',n-4,4)+  1/16*Px('1111',n-4,4)
	= 1/2*P(n-1,4) + 1/4*P(n-2,4) + 1/8*P(n-3,4) 
	   + 1/16*P(n-4,4)+ 1/16

The general solution is, therefore:

    P(n,k)=sum( 1/2^i * P(n-i,k) ) + 1/2^k
            (i=1..k)

##Solution based on the Fibonacci series

According to this source, it is possible to derive a solution based on the Fibonacci series for k=2:

	P(n,2) = (2^n-Fibonacci(n+2))/2^n

Therefore, it may also be possible to generalize a solution based on the Fibonacci series for k > 2.

