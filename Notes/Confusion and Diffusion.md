Two properties Shannon identified as necessary for a secure cipher. Modern systems like [[AES]] are designed around achieving both.

### Confusion

The relationship between plaintext and ciphertext should be complex and nonlinear. A small change in the key should produce unpredictable changes in the ciphertext. Achieved by **substitution**.

### Diffusion

Each plaintext element should influence many ciphertext elements, spreading information across the whole output. No single ciphertext element should depend on just one plaintext element. Achieved by **transposition/permutation**.

### Avalanche Effect

A consequence of good confusion and diffusion: flipping a single bit in the plaintext or key should change roughly half the ciphertext bits. Without this, an attacker can make small adjustments and observe small output changes to gradually narrow down the key.

### Why Both Are Needed

Substitution alone (confusion without diffusion) preserves positional relationships - each ciphertext element still maps to exactly one plaintext position. Transposition alone (diffusion without confusion) preserves the actual symbols and their frequency distribution. Only the combination breaks both statistical relationships. This is why [[Classical Ciphers]] evolve into product ciphers (substitution then transposition), and why modern block ciphers run many rounds of both.

See also:
- [[Classical Ciphers]]
- [[Cryptography]]
- [[AES]]
- [[Cryptanalysis]]
