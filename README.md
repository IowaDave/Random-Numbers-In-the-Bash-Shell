# Random Numbers in the Bash Shell
Discovering ways to get random numbers for use in scripts and programs written for the *bash* shell of a Gnu/Linux computer.

## Quick and Dirty For Readers In A Hurry

1. The classic, built-in, 16-bit variable, RANDOM
<code><pre>myVar=$RANDOM
echo $myVar
</pre></code>

2. Writing a &ldquo;seed&rdquo; value to RANDOM causes it 
to repeat a definite sequence of seemingly random numbers
<code><pre>RANDOM=12345
echo $RANDOM
echo $RANDOM
RANDOM=12345 # repeat the seed
echo $RANDOM
echo $RANDOM
</pre></code>

3. The new (in 2020), improved, built-in, 32-bit variable, SRANDOM
<code><pre>myVar=$SRANDOM
echo $myVar
</pre></code>

Note: SRANDOM cannot be seeded, which means that program code
cannot instruct it to repeat a definite sequence of values.

4. An UberGeek way, with a pipeline from the automatic random-number file named /dev/urandom
<code><pre>myVar=$(dd if=/dev/urandom count=1 bs=4 status=none | od -t u4 -A n | tr -d ' ')
echo $myVar
</pre></code>

The ```bs=4``` and ```u4``` options in the above calls to dd and od,
respectively, result in 4-byte, 32-bit unsigned random integers.
Changing those options can change the size (in bits) of the result.
Valid alternatives are:

* The pair, bs=1 u1, give a one-byte, 8-bit result

* bs=2 u2 give a two-byte, 16 bit result

* On systems supporting 64-bit integers,
bs=8 and u8 will give 64-bit random integers.

In November 2026 the author began writing an article
discussing these methods and providing examples usage.
Shell scripts have been designed to simulate flipping a coin,
rolling dice, shuffling cards, selecting numbers for a certain lottery,
and drawing Bingo balls.

The main challenge in writing is to keep it short.
This author approaches it in steps: first write a long article; then
cut it down to size. The second step takes longer.
