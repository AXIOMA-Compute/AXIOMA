# AXIOMA/Compute Specification
Version 0.1

---

## 1. Terminology

**Constraint:**  
A mathematical condition describing valid state transitions.

**Worker:**  
An entity performing external computation.

**Proof:**  
A cryptographic proof validating the correctness of the worker's computation.

**Verifier:**  
Protocol component responsible for proof validation.

---

## 2. Valid State Transition

A state transition is valid if and only if:

```
Verify(proof, result) == true
AND
ConstraintsSatisfied(result, previous_state) == true
```

Invalid transitions MUST NOT modify state.

---

## 3. External Compute Interface

Workers submit:

```
compute_packet {
    input_hash,
    output_value,
    proof
}
```

Protocol MUST:

1. Validate proof  
2. Validate constraints  
3. Apply deterministic state update  

---

## 4. Constraint System

Constraints MAY be represented as:

- R1CS  
- AIR (STARK-compatible)  
- Plonkish constraint languages  
- A domain-specific constraint DSL  

Constraints define:

- invariant maintenance  
- allowed state machines  
- required relationships between inputs and outputs  

Constraints MUST be immutable unless governed by a deterministic upgrade mechanism.

---

## 5. Verifier Behavior

The verifier MUST:

- reject malformed proofs  
- reject proofs not matching constraints  
- reject unverifiable inputs  
- treat invalid proofs as a no-op  

Verification MUST be deterministic.

---

## 6. Deterministic State Machine

State MUST be updated only when all validations pass.

State = f(previous_state, validated_result)

---

## 7. JAM Integration

AXIOMA/Compute supports two transition types:

```
1. Internal Transition:   state' = JAM(state, input)
2. External Transition:   state' = AXIOMA(state, proof)
```

Both MUST converge to identical deterministic state behavior.

---

## 8. Security Assumptions

- soundness of the proof system  
- collision resistance of hash functions  
- immutability of constraint definitions  

---

## 9. Consensus Layer Compatibility

AXIOMA/Compute is consensus-agnostic.  
It can operate on any protocol offering:

- deterministic state application  
- reproducible execution  
- data availability  

---

## 10. Future Extensions

- recursive prover networks  
- distributed compute marketplaces  
- deterministic AI inference layers  
- hardware-accelerated proving modules  

## 11. Quantum Threat Model

This section defines the security assumptions of AXIOMA/Compute under the presence of quantum-capable adversaries.

---

### 11.1 Scope

A quantum adversary is defined as an entity capable of performing computation using large-scale fault-tolerant quantum hardware with access to algorithms such as:

- Shor’s algorithm (for factoring & discrete logarithms)
- Grover’s algorithm (for quadratic search speedups)
- quantum-accelerated arithmetic operations

The goal of this section is to specify which AXIOMA/Compute components remain secure under quantum capabilities.

---

### 11.2 Components Not Affected by Quantum Adversaries

Quantum computers **cannot** violate or bypass the following:

1. **Mathematical Constraints**  
   Constraints are logical relationships, not “hard problems.”  
   Quantum hardware cannot produce a mathematically valid output unless it is genuinely correct.

2. **State Transition Validity**  
   The correctness condition:
   ```
   Verify(proof, result) == true
   AND
   ConstraintsSatisfied(result, state) == true
   ```
   cannot be coerced or forced by quantum computation.

3. **STARK Proof Systems**  
   AXIOMA/Compute uses transparent, hash-based proof systems.  
   These do not depend on elliptic curves or discrete log assumptions.  
   STARKs remain secure under quantum attacks because:
   - hashes remain resistant (Grover reduces bit-security by factor 2 only)
   - AIR constraints are algebraic, not factorization-based
   - FRI low-degree testing is not weakened by quantum models

4. **Constraint Enforcement**  
   A quantum adversary cannot:
   - forge an algebraic execution trace  
   - falsify low-degree consistency proofs  
   - bypass boundary constraints  
   - manipulate the verifier  

---

### 11.3 Components Potentially Affected by Quantum Adversaries

The following components require explicit quantum-safe design:

1. **Digital Signatures (Identity Layer)**  
   Classical signatures (ECDSA, Ed25519, sr25519) are vulnerable.
   AXIOMA/Compute MUST use quantum-safe alternatives, e.g.:
   - Dilithium
   - Falcon
   - SPHINCS+
   - XMSS (hash-based)

2. **Hash Function Security Margin**  
   Grover’s algorithm reduces effective bit-security.  
   AXIOMA/Compute MUST use hash functions with sufficient overhead:
   - SHA-256 → provides ~128-bit post-quantum security
   - Blake3 → >128-bit post-quantum
   - Poseidon / Rescue variants with adequate field sizes

3. **Key Agreement (if used)**  
   Elliptic curve–based key exchange is not quantum-safe.  
   If key agreement is part of any extension, it MUST use:
   - Kyber  
   - NTRU  
   - FrodoKEM  

---

### 11.4 Forbidden Cryptographic Dependencies

AXIOMA/Compute MUST NOT depend on:

- RSA  
- ECDSA  
- ECDH  
- elliptic curve pairing assumptions  
- Groth16 SNARKs with toxic waste  
- any proving system requiring trusted setup or discrete-log hardness  

These systems are vulnerable to quantum attacks and incompatible with AXIOMA’s threat profile.

---

### 11.5 Security Assumptions Under Quantum Adversaries

AXIOMA/Compute remains secure under the following assumptions:

1. **Hash-based commitments remain collision-resistant**  
   (quantum reduction accounted for)

2. **STARK proof soundness remains unaffected**

3. **Constraint satisfaction is purely mathematical and cannot be brute-forced**

4. **Verification remains deterministic and reproducible**

5. **Signature layer is replaced with quantum-safe alternatives**

---

### 11.6 Summary

AXIOMA/Compute is inherently resilient to quantum adversaries when implemented with:

- transparent STARK proofs  
- hash-based commitments  
- quantum-resistant signatures  
- no reliance on elliptic curve cryptography  

Quantum computers can *accelerate* external computation,  
but they cannot:

- forge proofs  
- violate constraints  
- manipulate state  
- bypass the verifier  

AXIOMA/Compute remains fully secure in a post-quantum world.
