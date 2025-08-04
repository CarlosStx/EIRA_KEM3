# EIRA-KEM: Post-Quantum Key Encapsulation Mechanism

This repository contains an academic implementation of **EIRA-KEM**, a symbolic algebra-based key encapsulation mechanism designed for post-quantum cryptography.

## Description

EIRA-KEM uses symbolic matrix algebra, high-entropy randomness, and AES-GCM-based authenticated encryption to securely exchange symmetric keys. The construction is post-quantum by design and offers high flexibility in key sizes and performance.

## Usage

This implementation is provided **for academic and non-commercial research purposes only**. You may test, benchmark, analyze, or modify the code for scientific exploration or educational use.

**Do not use this code in commercial products or services without written permission.**

## Legal Notice

EIRA-KEM is part of a **patent-pending cryptographic system**, filed under **PCT reference WO/2025/057369**.  
All commercial rights reserved © 2025 Carlos Santacruz.

## Contact

For licensing, integration, or academic collaboration:
**csantacruze@yahoo.com.mx**


## 🔍 EIRA-KEM Protocol Internals and Symbolic Structure

EIRA-KEM is a symbolic post-quantum key encapsulation mechanism (KEM) that uses symbolic entropy matrices, AES-GCM encryption, and HKDF key derivation.

###  Key Objects
- `sk`: a symbolic seed (the private key) — an algebraic description including entropy source, symbolic rules, and expression generators.
- `pk`: a symbolic matrix deterministically derived from `sk`.
- `r`: a random ephemeral secret generated during encapsulation.
- `K`: a session key derived from `HKDF(r || pk)`.
- `ciphertext`: AES-GCM encryption of `r` using part of `K`.

###  Encapsulation Process
1. The sender derives a symbolic matrix `pk = SymbolicMatrix(sk)`.
2. A fresh ephemeral `r` is generated.
3. A shared session key `K = HKDF(r || pk)` is derived.
4. `r` is encrypted using AES-GCM with a portion of `K`, producing `ciphertext`.
5. The sender transmits `(ciphertext, pk)` to the receiver.

###  Decapsulation Process
1. The receiver reconstructs `pk` using `sk` (symbolic rules).
2. Decrypts `ciphertext` using AES-GCM and part of `K`.
3. Recovers `r` and derives the session key `K = HKDF(r || pk)`.

###  Security Assumption: Symbolic Inversion Problem

The hardness of EIRA-KEM lies in the symbolic inversion problem:

> Given a symbolic matrix `pk`, it is computationally infeasible to recover the underlying symbolic generation seed `sk`, or to predict a valid `r'` such that `HKDF(r' || pk)` matches the actual session key `K`, without knowledge of `sk`.

This problem class is distinct from number-theoretic assumptions (LWE, RSA) and instead relies on the structural unpredictability of entropy-driven symbolic algebraic expressions.

This symbolic hardness assumption defines the asymmetric nature of EIRA-KEM.

###  Example Construction (simplified)
A symbolic matrix might be constructed as:

M[i][j] = ((α * i + β * j)^e + γ) mod p

Where α, β, γ, e are symbolic constants seeded from high-entropy sources. Reconstructing these from `M` without `sk` is the basis of the symbolic inversion challenge.

EIRA-
