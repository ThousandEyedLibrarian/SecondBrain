Data Encryption Standard. The previous [[Symmetric Encryption]] standard, used widely from 1976 until replaced by [[AES]].

### Specs

- Feistel structure
- 64-bit block size
- 56-bit effective key (64 bits minus 8 parity bits)
- 16 rounds, each with its own 48-bit subkey

### Round Function

Each round processes the 32-bit right half through four steps:
1. **Expansion** - 32 bits to 48 bits (duplicates some bits, increases diffusion)
2. **XOR with round key** - mixes in the 48-bit subkey
3. **S-box substitution** - 8 boxes, each 6 bits in / 4 bits out. Nonlinear. These are the main source of security in DES.
4. **Permutation** - shuffles bit positions (more diffusion)

After round 5, every output bit depends on every input bit and every key bit (full avalanche). The remaining 11 rounds further complicate the mathematical relationship to resist differential and linear [[Cryptanalysis]].

### Why It's Broken

56-bit key = 2^56 possible keys (about 72 quadrillion). Sounds big, but the EFF cracked it in 56 hours in 1998 with a purpose-built $250k machine. Modern hardware would be vastly faster. The key space is simply too small.

### Triple DES (3DES)

The stopgap fix: run DES three times with three different keys (encrypt-decrypt-encrypt). Effective key length of 168 bits, reduced to 112 bits in practice due to meet-in-the-middle attacks. Still limited by DES's 64-bit block size and three times the computation cost, which is why [[AES]] replaced it.

See also:
- [[AES]]
- [[Symmetric Encryption]]
- [[Confusion and Diffusion]]
- [[Cryptanalysis]]
