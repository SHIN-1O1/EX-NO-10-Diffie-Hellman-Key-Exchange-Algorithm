# EX-NO-10-Diffie-Hellman-Key-Exchange-Algorithm

## AIM:
To Implement Diffie Hellman Key Exchange Algorithm 

## Algorithm:

1. Diffie-Hellman Key Exchange is used for securely sharing a secret key between two parties over an insecure channel.

2. Initialization: Agree on a large prime number \( p \) and a primitive root \( g \) modulo \( p \) (both are public values).

3. Key Exchange Process: 
   - Each party selects a private key and calculates their public key using the formula \( g^{\text{private key}} \mod p \).
   - Each party then shares their public key with the other.

4. Secret Key Computation: 
   - Each party computes the shared secret key using the received public key and their own private key.

5. Security: The difficulty of computing discrete logarithms ensures that the shared key remains secure even if public values are intercepted.

## Program:
```
#include <stdio.h>
#include <stdlib.h>

/* Compute (a^b) % mod using fast modular exponentiation */
unsigned long long mod_pow(unsigned long long a, unsigned long long b, unsigned long long mod) {
    unsigned long long result = 1;
    a %= mod;
    while (b > 0) {
        if (b & 1ULL) result = (result * a) % mod;
        a = (a * a) % mod;
        b >>= 1;
    }
    return result;
}

int main(void) {
    unsigned long long P, G;
    unsigned long long a, b;           /* private keys */
    unsigned long long x, y;           /* public keys */
    unsigned long long ka, kb;         /* shared secrets */

    printf("***** Diffie-Hellman Key Exchange (demo) *****\n\n");

    printf("Enter the value of P (a prime number): ");
    if (scanf("%llu", &P) != 1) return 1;
    printf("P = %llu\n", P);

    printf("Enter the value of G (a primitive root modulo P): ");
    if (scanf("%llu", &G) != 1) return 1;
    printf("G = %llu\n\n", G);

    /* Example: choose private keys (in practice choose them randomly) */
    printf("Enter private key for Priya (a): ");
    if (scanf("%llu", &a) != 1) return 1;

    printf("Enter private key for Dharshini (b): ");
    if (scanf("%llu", &b) != 1) return 1;

    /* Compute public keys */
    x = mod_pow(G, a, P);  /* Priya's public key */
    y = mod_pow(G, b, P);  /* Dharshini's public key */

    printf("\nPriya's public key (x = G^a mod P): %llu\n", x);
    printf("Dharshini's public key (y = G^b mod P): %llu\n\n", y);

    /* Each computes the shared secret */
    ka = mod_pow(y, a, P); /* Priya computes (y^a mod P) */
    kb = mod_pow(x, b, P); /* Dharshini computes (x^b mod P) */

    printf("Shared secret computed by Priya:     %llu\n", ka);
    printf("Shared secret computed by Dharshini: %llu\n", kb);

    if (ka == kb) {
        printf("\nSuccess: both parties share the same secret.\n");
    } else {
        printf("\nWarning: shared secrets differ — something went wrong.\n");
    }

    return 0;
}

``` 



## Output:
<img width="804" height="607" alt="image" src="https://github.com/user-attachments/assets/a712daf5-bf27-4808-8ce9-628e122c7613" />




## Result:
  The program is executed successfully

