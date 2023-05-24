# **Cybersecurity ECC Encryption**
#### By Jefford Shau & Kosta Dubovskiy
---
## **What is Elliptic Curve Cryptography (ECC) Encryption?**
 - Public key encryption technique based on the elliptic curve theory
 - Trapdoor One-Way Function
     - Easy to encode but difficult to decode

---
## **Fundamentals of ECC Encryption:**

## **Characteristics of Elliptic Curves**
 - Set of points that satisfy the equation y²=x³+ax+b
 - Symmetric about the x-axis
 - Straight lines intersect the curve at no more than 3 points

 ![Elliptic Curve](https://github.com/Stuycs-K/final-project-4-shauj-dubovskiyk/blob/main/images/elliptic_curve.png)

 ## **Parameter P**

 // something about mod

 ## **Parameter G**

 - Predetermined point (xG, yG) on the curve that everyone uses to compute other points on the curve
 - Starting point/base point
 - Displayed in two ways:
    - Compressed form (only x-coordinate is stored)
        - xG = 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B (Prefix 02)
        - yG = (xG + 7)^(½)
    - Uncompressed form (stores both x-coordinate and y-coordinate)
        - <span style="background-color: #191970">79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798</span> <span style="background-color: #FF0000">483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A6855419 9C47D08F FB10D4B8</span> (Prefix 04)
        - xG = Blue
        - yG = Red

## Point Addition
- If a line intersects two points P and Q, it intersects one other point on the curve at -R
- Geometric Approach
    - Let P = (x1, y1) and Q = (x2, y2)
    - Draw a straight line PQ intersects the curve at -R (x3, -y3)
    - Reflection point -R across the x-axis resulting in point R (x3, y3)
    - P + Q = R
- Point Multiplication
    - Repeated point addition
    - nP = P + P + P + … (n+1) operations

## Point Doubling
- If a line is tangent to the curve, it intersects one other point on the curve at -R
- Geometric Approach
    - Let P = (x1, y1) and P = Q
    - Draw a tangent line that intersects the curve at point P
    - The line intersects exactly one other point on the curve at point R (x3, y3)
    - Reflection point -R across the x-axis resulting in point -R (x3, -y3)
    - 2P = R

## Special Case: Point at Infinity
- If the tangent line to the curve at point P is vertical, it intersects the curve at -P 
- Geometric Approach
    - Let P = (x1, y1) and P = Q
    - Draw a vertical tangent line that intersects the curve at point -P
    - Reflection point P across the x-axis resulting in point -P (x1, -y1)


## Point Negation

// insert here

---

## **Public and Private Keys**
- Q = nG
    - Q: public key coordinates (x, y)
    - n: private key (large integer)
    - G: parameter G, generator key (x, y)
- Key Operations Ladder (right to left)
- “0” bit - double points
- “1” bit - add and double points

## **Diffie-Hellman Key Exchange**

Step | Alice| Mutual | Bob
--- | --- | :---: | ---
1 | _ | Decide on parameter G privately | _
2 | Private key: A | _ | Private key: B
3 | Public key: A * G | _ |Public key: B * G
4 | _ | Exchange public keys and multiply keys by their own private keys | _ 
5 | Shared encrypt/decrypt key:    A * (B * G)	| _ | Shared encrypt/decrypt key:     B * (A * G)
- Hackers may intercept public keys but difficult to determine private keys

---

## **Advantages of ECC Encryption**

 - Creates keys using less computation power and battery power than Rivest–Shamir–Adleman (RSA) encryption
 - Reduced key size compared to RSA encryption results in less storage used
 - Stronger algorithm than Diffie-Hellman and RSA encryption
     - 256-bit elliptic curve key provides same level of security as 3072-bit RSA key
 - Used often for mobile devices
     - Heavy computational factoring algorithms in RSA encryption not ideal for mobile devices

---

## Real-World Applications of ECC

 - Protect confidential government information by the US Government
    - 300+ bit key sizes
 - The Onion Router (Tor)
    - Open-source software for anonymous communication
 - Proving Bitcoin Ownership
 - Apple’s iMessage signatures and other digital signatures
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
 - One-way encryption of emails, data, and software
 - Mobile providers

---

## **Implementing ECC Encryption**

// insert here

## **Concerns of ECC Encryption**

Most Elliptic Curves are Patented
Theoretical Solution
No algorithmic solution in the last three decades yet
Quantum Computing Attacks
Bad RNG leads to successful attacks

## **Why ECC is Not Commonly Used**

// insert here

---
## **Conclusion**

// insert here

## **Homework**

// insert here

