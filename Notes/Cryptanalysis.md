The study of breaking cryptographic systems without knowing the key. Paired with [[Cryptography]] under the umbrella of cryptology.

### Attack Types

Ranked by how much information the attacker has, weakest to strongest:

1. **Ciphertext only (COA)** - attacker only has ciphertext. Frequency analysis works here against weak ciphers.
2. **Known plaintext (KPA)** - attacker has some plaintext-ciphertext pairs they didn't choose. Bletchley Park exploited this against Enigma using predictable message openings like weather report headers.
3. **Chosen plaintext (CPA)** - attacker picks plaintexts and observes the ciphertexts. Allows strategic probing of the system.
4. **Chosen ciphertext (CCA)** - attacker picks ciphertexts and observes the resulting plaintexts.
5. **Chosen text (CTA)** - attacker can do both. The strongest attacker model.

All of these assume the algorithm is public and only the key is secret (Kerckhoffs' principle). Security that depends on a hidden algorithm is not real security.

**Brute force** sits separately from these - just try every possible key. Feasibility depends entirely on key space size (25 keys for Caesar vs. 26! for monoalphabetic vs. 2^128 for [[AES]]).

### Frequency Analysis

The classic cryptanalytic technique. Works against any cipher where each plaintext letter always maps to the same ciphertext letter (monoalphabetic substitution). In English, E appears at roughly 12.7%, followed by T, A, O, I, N, S, H. Double and triple letter frequencies (like "th", "the") narrow things down further.

See also:
- [[Cryptography]]
- [[Classical Ciphers]]
- [[Information Security]]
