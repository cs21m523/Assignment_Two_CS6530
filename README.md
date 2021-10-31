# Assignment Two CS6530

Name: Mann Jani
Roll Number: CS21M523


##### 8.2 a. What is the maximum period obtainable from the following generator?  
##### <pre>       X<sub>n+1</sub> ≡ (aX<sub>n</sub>) mod 2<sup>4</sup> </pre>
The maximum period is 2<sup>4</sup> / 4 = 4.  
##### b. What should be the value of a?
The maximum period is achievable when a ≡ 3 mod 8 or a ≡ 5 mod 8. Which means possible values for a are 3, 5, 11  

##### c. What restrictions are required on the seed?
The initial seed X<sub>0</sub> must be odd.

##### 8.4 With the linear congruential algorithm, a choice of parameters that provides a full period does not necessarily provide a good randomization. For example, consider the following two generators:
##### <pre>       X<sub>n+1</sub> ≡ (11X<sub>n</sub>) mod 13 </pre>
##### <pre>       X<sub>n+1</sub> ≡ (2X<sub>n</sub>) mod 13 </pre>
##### Write out the two sequences to show that both are full period. Which one appears more random to you?
Starting with initial seed 1, the first generator has the sequence:
<pre> 1, 11, 4, 5, 3, 7, 12, 2, 9, 8, 10, 6, 1, ...</pre>
Starting with initial seed 1, the second generator has the sequence:
<pre> 1, 2, 4, 8, 3, 6, 12, 11, 9, 5, 10, 7, 1, ...</pre>
Since the second sequence appears to have a recognizable pattern initially, it appears less random compared to the first sequence.

##### 8.6 What RC4 key value will leave S unchanged during initialization? That is, after the initial permutation of S, the entries of S will be equal to the values from 0 through 255 in ascending order?
Using a key of 256 bytes where K[0] = 0 and K[1] = 0, and there after K[2] = 255, K[3] = 254, ..., K[255] = 2.  
Explanation:  
Since length of the key is 256 bytes - K is transferred to T. Which means
S[0] = 0, S[1] = 1, S[2] = 2, ..., S[255] = 255
T[0] = 0, T[1] = 0, T[2] = 255, ..., T[255] = 2

The initial permutation algorithm is:
j = 0;  
for i = 0 to 255 do
    j = (j + S[i] + T[i]) mod 256;
    Swap (S[i], S[j])

To leave S unchanged, the value of j must be equal to i at each iteration. Which is true for given key.

##### 8.7 RC4 has a secret internal state which is a permutation of all the possible values of the vector S and the two indices i and j.
##### a. Using a straightforward scheme to store the internal state, how many bits are used?
We can directly store i, j and S, which means the total number of bits required are 8 for i, 8 for j and 256 * 8  = 2048 for S. Total is 2064 bits.
##### b. Suppose we think of it from the point of view of how much information is represented by the state. In that case, we need to determine how many different states there are, then take the log to base 2 to find out how many bits of information this represents. Using this approach, how many bits would be needed to represent the state.
The number of states for S are 256!, possible values of i are 0 to 255 and possible values of j are 0 to 255.  
Which means the total number of states is 256! * 256 * 256 ~= 2<sup>1700</sup>  
So, using this approach 1700 bits would be needed to represent the state.

##### 8.8 Alice and Bob agree to communicate privately via email using a scheme based on RC4, but they want to avoid using a new secret key for each transmission. Alice and Bob privately agree on a 128-bit key k. To encrypt a message m, consisting of a string of bits, the following procedure is used.
##### 1. Choose a random 64-bit value v
##### 2. Generate the ciphertext c = RC4(v || k) ⊕ m
##### 3. Send the bit string (v || c)
##### a. Suppose Alice uses this procedure to send a message m to Bob. Describe how Bob can recover the message m from (v || c) using k.
By taking the first 64 bits from (v || c), Bob can recover the random value v ( || is concatenation operator ).  
Rest of the bits of (v || c) are c.  
Since now Bob knows v (from encrypted message v || c ), c (from encrypted message v || c), and k (previously agreed upon with Alice). Bob can recover the original message m by computing m = RC4(v || k) ⊕ c.
##### b. If an adversary observes several values (v<sub>1</sub> || c<sub>1</sub>), (v<sub>2</sub> || c<sub>2</sub>), ... transmitted between Alice and Bob, how can he/she determine when the same key stream has been used to encrypt two messages?
If the adversary observes that two encrypted messages (v<sub>1</sub> || c<sub>1</sub>) and (v<sub>2</sub> || c<sub>2</sub>) have the same prefix, he/she can determine that the same key stream has been used to encrypt two messages.
##### c. Approximately how many messages can Alice expect to send before the same key stream will be used twice? Use the result from the birthday paradox described in Appendix U.
Since key is fixed, the key stream varies with the random value v. Size of possible values of v is 2<sup>64</sup>. According to birthday paradox, the probability of v being repeated exceeds 50% chance after 2<sup>64/2</sup> values. So Alice can expect to send 2<sup>32</sup> messages before the same key stream will be used twice with a high probability.
##### d. What does this imply about the lifetime of the key k (i.e. the number of messages that can be encrypted using k)?
This implies that the lifetime of key k is about 2<sup>32</sup> messages, after that k should be changed.

##### 8.5 In any use case of pseudorandom numbers, whether for encryption, simulation, or statistical design, it is dangerous to trust blindly the random number generator that happens to be available in your computer's system library. [PARK88] found that many contemporary textbooks and programming packages make use of flawed algorithms for pseudorandom number generation. This exercise will enable you to test your system.

##### The text is based on a theorem attributed to Ernesto Cesaro (see [KNUT98] for a proof), which states the following: Given two randomly chosen integers, x and y, the probability that gcd(x, y) = 1 is 6/&pi;<sup>2</sup>. Use this theorem in a program to determine statistically the value of &pi; The main program should call three subprograms: the random number generator from the system library to generate the random integers; a subprogram to calculate the greatest common divisor of two integers using Euclid's Algorithm; and a subprogram that calculates square roots. If these latter two programs are not available, you will have to write them as well. The main program should loop through a large number of random numbers to give an estimate of the aforementioned probability. From this, it is a simple matter to solve for your estimate of &pi;.

##### If the result is close to 3.14, congratulations! If not, then the result is probably low, usually a value of around 2.7. Why would such an inferior result be obtained?
See attached program program.c and program.exe.
Steps to compile: gcc -o program.exe program.c
Steps to execute: ./program.exe
