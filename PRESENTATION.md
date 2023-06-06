 # **Cybersecurity ECC Encryption**
 #### By Jefford Shau & Kosta Dubovskiy

 ---

 ## **What is Elliptic Curve Cryptography (ECC) Encryption?**

 - Public key encryption technique based on the elliptic curve theory
 - Trapdoor One-Way Function
     - Easy to encode but difficult to decode

 ---

 ## **Characteristics of Elliptic Curves**

 - Set of points that satisfy the equation y² = x³ + *a*x + *b*
 - 4*a*³ + 27*b*² ≠ 0 
     - Results in a singular curve with discriminant = 0 that is easy to solve
     - Graph has cusps, nodes (self-intersections), or acnodes (isolated points)
 - Symmetric about the x-axis
 - Straight lines intersect the curve at no more than 3 points

 ![Elliptic Curve](https://github.com/Stuycs-K/final-project-4-shauj-dubovskiyk/blob/main/images/elliptic_curve.png)

 ## **Dot Operations**

 ### **Point Addition**
 - If a line intersects two points P and Q, it intersects only one other point on the curve at -R
 - Geometric Approach
     - Let P = (x1, y1) and Q = (x2, y2)
     - Draw a straight line PQ intersecting the curve at R (x3, y3)
     - Reflection point R across the x-axis resulting in point -R (x3, -y3)
     - P + Q = -R
 - Special Cases
     - P = -Q (vertical line point negation)
         - Does not intersect any third point
         P + Q = P + (-P) = 0 (point at infinity)
     - P = 0 or Q = 0 (identity element)
         - P + 0 = P and 0 + Q = Q for any P and Q
     - P ≠ Q and no third point R
         - If P is the point of tangency, then P + Q = -P

 ### **Point Doubling** 
 - Special case of point addition that occurs very frequently
 - If a line is tangent to the curve, it intersects only one other point on the curve at -R
 - Geometric Approach
    - Let P = (x1, y1) and P = Q
    - Draw a tangent line that intersects the curve at point P
    - The line intersects exactly one other point on the curve at point R (x3, y3)
    - Reflection point -R across the x-axis resulting in point -R (x3, -y3)
    - 2P = R

 ### **Point Multiplication**
 - Repeated Point Addition
     - nP = P + P + P + … *(n times)*
     - If *n* has *k* binary digits, then the time complexity would be *O*(2<sup>k</sup>)
         - Faster algorithms exist
 - Scalar Multiplication (Double and Add Algorithm)
     1. Convert *n* from decimal to binary representation
     2. Take *P* and starting with the least significant digit (big endian right to left): 
         - “0” bit - double *P*
         - “1” bit - double and add *P*
     - If point addition and doubling are both *O*(1) operations, the double and add algorithm is *O*(log<sub>2</sub> *n*) 

 ---

 ## **Domain Parameters**

 ### **Parameter P**

 - Used in the expression y² = x³ + *a*x + *b* mod *p* to create a finite field(denoted F<sub>p</sub>, or Z/*p*) with domain 0 to *p*-1
 For every *x* value, there are at most **2** points — ± (x³ + *a*x + *b* mod *p*) 
 - Graph has symmetry about y = *p* / 2
 - The set of multiples of *p* is a cyclic subgroup formed by the elliptic curve
     - Important concept for Elliptic Curve Diffie-Hellman (ECDH)

#### **A Note On Finite Fields**
- In fields we have two binary operations: 
  - addition (+) 
  - multiplication (·)
- Both are closed, associative and commutative
- For both operations, there exist:
  - A unique identity element
  - A unique inverse element
-  Finally, multiplication is distributive over the addition

<u>Note</u>
- Note that the requirement for *p* to be prime is important!!
- The set of integers mod 4 is not a fields: for example, 2 has no multiplicative inverse(no solutions to 2 * x ≡ 1 mod 4)

 ### **Parameter G**

 - Predetermined point (xG, yG) on the curve that everyone uses to compute other points on the curve
 - Starting point/base point
 - Displayed in two ways:
    - Compressed form (only x-coordinate is stored)
        - xG = 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B (Prefix 02)
        - yG = (xG + 7)<sup>1/2</sup>
    - Uncompressed form (stores both x-coordinate and y-coordinate)
        - <span style="background-color: #191970">79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798</span> <span style="background-color: #FF0000">483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A6855419 9C47D08F FB10D4B8</span> (Prefix 04)
        - xG = Blue
        - yG = Red

 ---

 ## **Public and Private Keys**

 - Q = nG
    - Q: public key coordinates (x, y)
    - n: private key (large integer)
    - G: parameter G, generator key (x, y)

 ## **Diffie-Hellman Key Exchange**

 Step | Alice| Mutual | Bob
 --- | --- | :---: | ---
 1 | _ | Decide on parameter G privately(RSA, etc.) | _
 2 | Private key: A | _ | Private key: B
 3 | Public key: A * G | (* here is point multiplication, it's still very hard for bad actors to get A or B) |Public key: B * G
 4 | _ | Exchange public keys and multiply keys by their own private keys | _ 
 5 | Shared encrypt/decrypt key:    A * (B * G)	| _ | Shared encrypt/decrypt key:     B * (A * G)
 - Hackers may intercept public keys but difficult to determine private keys
 
 ---
 
 ## **Advantages of ECC Encryption**

 - Creates keys using less computation power, battery power than Rivest–Shamir–Adleman (RSA) encryption
 - Faster generation of keys
 - Smaller keys, ciphertext, and signatures size compared to RSA encryption results in less memory storage used
     - 256-bit elliptic curve key provides same level of security as 3072-bit RSA key
 - Used often for mobile devices
     - Heavy computational factoring algorithms are not ideal for mobile devices

 ---

 ## Real-World Applications of ECC

 - Protect confidential government information by the US Government
    - 300+ bit key sizes
 - The Onion Router (Tor)
    - Open-source software for anonymous communication
 - Proving Bitcoin Ownership
 - Apple’s iMessage signatures and other digital signatures such as PDFs
 - VPNs tunnel authentication and key exchange
    - OpenVPN
 - SSH Keys
    - `ssh-keygen ed25519`
    -  elliptic curve 25519 offers 128 bits of security (256-bit key size)
 - Encrypt Domain Name System (DNS) information through DNSCurve
 - Secure Sockets Layer (SSL)
    - Server and client handshaking protocol
 - Transport Layer Security (TLS)
    - Ensures the secure delivery of data over the Internet
    - Avoids possible eavesdropping and alteration of content
 - Internet Key Exchange (IKE)
 - One-way encryption of emails, data, and software
 - Mobile providers

 ---

 ## **Disadvantages of ECC Encryption**

 - Hard to implement
     - ECC private keys can be leaked when not implemented correctly
 - Relatively new technology compared to RSA
 - Most Elliptic Curves are Patented
     - Legal risk
 - Possible Quantum Computing Attacks
     - Shor's algorithm makes factoring easier
     - Grover's algorithm makes searching through unstructured data easier
     - ECC easier to crack than RSA due to shorter key lengths
 - Bad RNG leads to successful attacks
 - Side-channel attacks
     - Exploiting and analyzing information leaking from physical and virtual cryptoystems
         - Information to analyze: execution time, power consumption, supply curent, electromanetic and acoustic emissions
     - Ex: Observing differences in time between power consumption peaks with an oscilloscope
 - Twist-security attacks
     - Carefully selected public key not on the ECC curve causes a shared key that is easily reversible to be generated
     - Leaks the victim's private key
 - Speculation the National Security Agency (NSA) added a backdoor as an ECC standard
     - Flaws and leaked seeds in random number generators make "random" numbers easy to predict
 
 ---

 ## **Homework**

 Code your own point addition and point doubling!

