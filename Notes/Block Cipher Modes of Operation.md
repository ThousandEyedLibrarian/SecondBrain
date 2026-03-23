Block ciphers encrypt fixed-size blocks, but real messages are arbitrary length. Modes of operation define how to handle this. The choice of mode matters as much as the choice of algorithm - [[AES]] with a bad mode still leaks information.

### ECB (Electronic Codebook)

Each block encrypted independently with the same key. Identical plaintext blocks produce identical ciphertext blocks, so patterns in the data are visible in the ciphertext. The encrypted penguin problem - structure is preserved even though values change. Never use for anything where patterns matter.

### CBC (Cipher Block Chaining)

XOR each plaintext block with the previous ciphertext block before encrypting. First block XORs with a random initialisation vector (IV). Identical plaintexts now produce different ciphertexts. Most commonly used mode historically.

Trade-offs: can't encrypt in parallel (each block depends on the previous), losing a block corrupts the next block's decryption. IVs must never be reused with the same key - same IV + same first plaintext block = same first ciphertext block, leaking that the messages start identically.

### CFB (Cipher Feedback)

Similar to CBC but the XOR happens after encryption rather than before. Same advantages and disadvantages.

### OFB (Output Feedback)

Feeds back the cipher output (before the XOR) rather than the ciphertext. The keystream can be precomputed before the plaintext is available, effectively turning the block cipher into a stream cipher.

### CTR (Counter)

Encrypt an incrementing counter value, XOR the result with plaintext. Each block is independent, so you get parallel encryption with no pattern leakage. Widely used in practice for this combination of security and performance.

See also:
- [[AES]]
- [[DES]]
- [[Symmetric Encryption]]
- [[Cryptography]]
