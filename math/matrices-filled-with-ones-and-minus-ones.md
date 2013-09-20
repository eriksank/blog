#Matrices filled with ones and minus ones

Yesterday, I ran into a really interesting question in the Google+ Mathematics community:

	Consider an n x n matrix. with each entry being +1 or -1. the product of the entries in
	each row & each column is -1. find the number of such matrices.

It looks like a simple question, but it happens to yield a few complications, that are actually quite interesting in themselves.

#1. Examples of the n x n matrices we are trying to count

So, what does the question mean? For example, for n=1, there is just one way to construct such matrix:

	[ -1 ]

The product across the rows is -1 and the across the columns too. We cannot place a 1 in this matrix, because the product won't be -1.

For example, for n=2, there are obviously two arrangements possible:

	[ -1  1 ]    or   [ 1  -1 ]
	[  1 -1 ]         [ -1 1  ]

An example for n=3:

	[  -1  1  1 ]
	[  -1 -1 -1 ]
	[  -1  1  1 ]

For the matrix to be a valid solution, the number of -1 in each row and in each column must be odd. So, what if we pick an arbitrary value for n. How many different arrangements would be possible for such matrix?

#2. Moving to binary matrices

The first step in the solution, is to replace 1 by 0 and -1 by 1, in order to move to binary numbers, and be able to use results from the boolean algebra. So, in boolean form, the example for n=3 becomes:

	[   1  0  0 ]
	[   1  1  1 ]
	[   1  0  0 ]

#3. Number of n-digit boolean numbers with an odd number of digits equal to 1

The next question becomes: How many n-digit boolean numbers with an odd number of digits equal to 1 can we construct?

All the boolean numbers with 1 digits are:

	0
	1 *

The answer for n=1 is: Just one.

The boolean numbers with 2 digits are:

	0 0
	0 1 *
	1 0
	1 1 *

The answer for n=1 is: two.

For n=3:

	0 - 0 0
	0 - 0 1 *
	0 - 1 0 *
	0 - 1 1
	1 - 0 0 *
	1 - 0 1
	1 - 1 0
	1 - 1 1 *

The answer for n=3 is 4.

Generally, the answer seems to be 2^(n-1). Why?

Look at the case for n=3. We can derive the case for n=3 from the case for n=2. We construct the first half by prefixing the case for n=2 by a zero:

	0 - 0 0
	0 - 0 1 *
	0 - 1 0 *
	0 - 1 1

It has exactly the same number of odd digits equal to 1 as the case for n=2, because adding a zero does not change anything to the count. We construct the second half by prefixing a 1 to the case for n=2:

	1 - 0 0 *
	1 - 0 1
	1 - 1 0
	1 - 1 1 *

By adding a 1, all numbers that had an odd number of digits equal to 1 for n=2, will now have an even number of digits equal to 1, while the ones which had an even number of digits equal to 1, will now have an odd count. So, now we can establish the recurrence relation for the count of odd digits for any n:

	f(n) = f(n-1) + (2^(n-1) - f(n-1)) , f(1)=1

This happens to be equivalent to:

	f(n) = 2 * f(n-1) , f(1)=1

We can solve either recurrence manually, or using a computer algebra system such as Maxima:

	load(solve_rec);
	solve_rec(f[n]=2*f[n-1],f[n],f[1]=1);

The result is, of course: f(n)=2^(n-1).

#4. Number of binary matrices satisfying the condition

So, now we can construct all possible matrices for n=3, by picking every possible repetition of 3-digit binary numbers with an odd number of digits: 001, 010, 100, 111. We can only freely choose the first two rows in the matrix, because the third row must ensure that the number of digits equal to one in each column is odd:

	[ 0 0 1 ] [ 0 0 1 ] [ 0 0 1 ] [ 0 0 1 ]
	[ 1 0 0 ] [ 0 1 0 ] [ 0 0 1 ] [ 1 1 1 ]
	[ 0 1 0 ] [ 1 0 0 ] [ 1 1 1 ] [ 0 0 1 ]
	[ 0 1 0 ] [ 0 1 0 ] [ 0 1 0 ] [ 0 1 0 ]
	[ 1 0 0 ] [ 0 1 0 ] [ 0 0 1 ] [ 1 1 1 ]
	[ 0 0 1 ] [ 1 1 1 ] [ 1 0 0 ] [ 0 1 0 ]
	[ 1 0 0 ] [ 1 0 0 ] [ 1 0 0 ] [ 1 0 0 ]
	[ 1 0 0 ] [ 0 1 0 ] [ 0 0 1 ] [ 1 1 1 ]
	[ 1 1 1 ] [ 0 0 1 ] [ 0 1 0 ] [ 1 0 0 ]
	[ 1 1 1 ] [ 1 1 1 ] [ 1 1 1 ] [ 1 1 1 ]
	[ 1 0 0 ] [ 0 1 0 ] [ 0 0 1 ] [ 1 1 1 ]
	[ 1 0 0 ] [ 0 1 0 ] [ 0 0 1 ] [ 1 1 1 ]

Since, we have to 2^(n-1) n-digit numbers and since we need to pick a repetition of n-1 such numbers for each result, the number of different matrices is:

	2^((n-1)^2)

#5. Validating the construction of the last row in the binary matrices

There is a condition, however. We cannot choose the last row. It is tasked to make sure that the count of digits equal to 1 in the columns is odd. While doing so, however, this last row must also automatically have an odd number of digits equal to 1. Will this always be the case?

It is again, the boolean algebra that comes to our rescue. If we look at how we construct the last row in each matrix:

	[ 1 1 1 ]  [ 1 0 0 ]
	[ 1 0 0 ]  [ 1 0 0 ]
	[ 1 0 0 ]  [ 1 1 1 ]

We can see that in order to guarantee an odd count in each column, we perform an XOR operation on the first two rows and apply a binary NOT to the result, in order to obtain the last row. For example for the first example matrix:

	NOT ( [ 1 1 1 ] XOR [ 1 0 0 ] ) = NOT ( [ 0 1 1 ] ) = [ 1 0 0 ]

For the second example:

	NOT ( [ 1 0 0 ] XOR [ 1 0 0 ]) = NOT ( [ 0 0 0 ] ) = [ 1 1 1 ]

This is the same as decimally adding up all elements in the row and then computing modulo 2 of the result and then apply the NOT operation:

	NOT (mod([ 1 1 1 ]+[ 1 0 0 ],2)) = NOT(mod([ 2 1 1],2)=NOT([0 1 1])=[ 1 0 0 ]
	NOT(mod([ 1 0 0 ]+[ 1 0 0 ],2)) = NOT(mod([2 0 0],2)=NOT([0 0 0])=[ 1 1 1 ]

We will now use boolean algebra to demonstrate that the last row always has an odd count of digits equal to 1.

#6. Properties of the XOR operator

When we XOR two arbitrary binary numbers, such as:

              digits equal to 1 
	       111101001     6
	   XOR 001110011     5
        ------------------          overlap                  
               110011010    11      - 2 x 3  = 5

If the first number has i digits equal to 1 and the second number has j digits equal to 1, we can see that the result will have i+j-2*k digits, with k the number of cases in which both numbers have the same digit equal to 1. The expression 2*k is always even. From basic number theory, we know:

	Rule                                          Example

	parity(odd+odd) = even                        3+5=8
	parity(even+odd) = odd                        3+4=7
	parity(even+even)=even                        4+2=6
	parity(odd-even) = odd                        7-2=5
	parity(even-even) = even                      6-4=2

For the parity of bits when applying the XOR operation, we can now demonstrate that:

	parity(i)=odd and parity(j)=odd: 
		parity(i XOR j) = parity(i+j - 2*k) 
		=odd+odd-even = odd + odd = even

In the same way we can demonstrate the following results:

case            result

odd XOR odd     even
even XOR even   even
even XOR odd    odd

Let's investigate examples in which we repeatedly apply the XOR operation to odd numbers. Fr example, we apply XOR 2 times in this example:

	parity(XOR^2 odd) = odd XOR (odd XOR odd)
	 = odd XOR even = odd

From the table above, we can see that:

	parity((XOR^k) (odd) | parity(k)=odd  ) = even
	parity((XOR^k) (odd) | parity(k)=even ) = odd

With the operator XOR^k designating the application of XOR k times.

#7. Properties of the NOT operator

We also need to investigate what happens to the parity of bits equal to 1, when applying a NOT operation. Example:

	                         n parity(n)  i  parity(i)   parity(NOT(i))

	NOT(001111)=110000       6  even      2  even         even
	NOT(11100) = 00111       5  odd       3  odd          odd

In table format, the general case is:

	parity: n              odd               even
	          odd           even [1]        odd [2]
		  even          odd  [3]        even [4]

Examples:

	[1] parity(NOT(00111)) = parity(11000) = even
	[2] parity(NOT(1000)) = parity(0111) = odd
	[3] parity(NOT(11000)) = parity(00111)=odd
	[4] parity(NOT(111100))=parity(000011)=even

#8. Properties of the XOR and NOT operator applied to the construction of the last row in the binary matrices

Using these properties, we can now finally investigate the construction of the last row in our matrices: For a matrix with n x n rows and columns, we construct the last row in the matrix by applying the following operations:

	NOT(XOR^(n-2) odd)

The parity of this operation is:

	parity(NOT(XOR^(n-2) odd))

The parity of the NOT operation depends on whether n is odd or even. Therefore, we have two cases:

	[1] parity(NOT(XOR^(n-2) odd) | parity(n)=even)
	= parity(NOT(XOR^even odd | parity(n)=even )
	= parity(NOT(odd) | parity(n)=even )
	= odd

[2] parity(NOT(XOR^(n-2) odd) | parity(n)=odd)
	= parity(NOT(XOR^odd odd) | parity(n)=odd)
	= parity(NOT(even) | parity(n)=odd)
	= odd

#9. Conclusion

The parity of the bits equal to 1 in the last row, will always be odd, regardless of whether n is odd or even. This demonstrates that the answer to the original question is indeed: 2^((n-1)^2).

