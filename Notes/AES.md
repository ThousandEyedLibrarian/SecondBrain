The current symmetric [[Encryption]] standard, replacing [[DES]]. Won a public NIST competition in 1997 - designed by Joan Daemen and Vincent Rijmen (Belgium), also called Rijndael.

### Specs

- 128-bit fixed block size
- Key sizes: 128, 192, or 256 bits
- Rounds: 10, 12, or 14 (scales with key size)
- Uses an SP (substitution-permutation) structure, not Feistel - the entire block is transformed each round

### Round Operations

Data is represented as a 4x4 byte matrix called the **state**. Each round applies four operations:

1. **SubBytes** - each byte is substituted through an S-box ([[Confusion and Diffusion|confusion]])
2. **ShiftRows** - rows are cyclically shifted by different amounts (diffusion)
3. **MixColumns** - each column is multiplied by a fixed matrix, so each output byte depends on multiple input bytes (diffusion)
4. **AddRoundKey** - XOR the state with the round key (key mixing)

The final round skips MixColumns.

### Why SP Instead of Feistel?

In a Feistel cipher like DES, only half the block is processed per round. SP processes the whole block, giving faster diffusion per round. The trade-off is that each step must be individually reversible (Feistel gets reversibility for free since one half is untouched).

### Security

Resistance to differential and linear [[Cryptanalysis]], power analysis, and other implementation attacks. At 128-bit keys, brute force requires roughly 3.4 x 10^38 operations - well beyond any foreseeable computing power.

See also:
- [[DES]]
- [[Confusion and Diffusion]]
- [[Classical Ciphers]]
- [[Block Cipher Modes of Operation]]
- [[Cryptography]]
