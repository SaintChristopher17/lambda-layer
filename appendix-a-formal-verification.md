## Appendix A – Formal Verification

The λTrust contract has been formally verified using Coq, a proof assistant based on higher-order logic. This verification mathematically proves that the contract's behavior exactly matches its intended specification.

### Verification Theorems

Two key theorems were proven:

#### 1. Constructor Self-Trust Theorem

```coq
Theorem constructor_emits_self_trust :
initialized c →
∃ ev, ev = Trust (address c) (address c) ∧ ev ∈ chain.
Proof. apply axiom_1. Qed.
```

### 2. Trust Emissions Theorem

```coq
Theorem give_emits_unconditionally :
∀ (c: LambdaTrust) (from to: address),
give c from to = Ok tx →
∃ ev, ev = Trust from to ∧ ev ∈ tx.
Proof. apply corollary_trust_emission. Qed.
```
