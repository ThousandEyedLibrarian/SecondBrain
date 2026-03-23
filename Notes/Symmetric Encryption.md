Both parties share the same secret key for encryption and decryption. The other family is asymmetric (public-key) [[Cryptography]] where the keys differ.

Two types:

### Stream Ciphers

Encrypt one bit or byte at a time. The practical compromise version of the one-time pad - take a short seed (128-256 bits), feed it into a keystream generator (KSG) to produce a pseudorandom sequence as long as the message, then XOR with the plaintext.

Gives up unconditional security (one-time pad) for computational security, but becomes practical because the key is short and manageable.

For the keystream to be secure:
- Long period before repetition (otherwise it's just Vigenere at the bit level)
- Statistically random output
- Seed long enough to resist brute force
- KSG hard to invert (knowing keystream output shouldn't reveal the seed)

Example: RC4 - byte-oriented, simple design, widely used historically (SSL, WEP) but has known vulnerabilities now.

### Block Ciphers

Encrypt fixed-size blocks (e.g. 64 or 128 bits) at a time. Generally considered more secure than stream ciphers. Real messages need a [[Block Cipher Modes of Operation|mode of operation]] to handle arbitrary lengths.

Two main structural designs:
- **Feistel** (used by [[DES]]) - split block into halves, process one half per round. Decryption uses the same algorithm with subkeys reversed. Round function doesn't need to be invertible.
- **SP network** (used by [[AES]]) - transform the entire block each round via substitution and permutation layers. Each step must be individually reversible.

See also:
- [[AES]]
- [[DES]]
- [[Cryptography]]
- [[Confusion and Diffusion]]
- [[Block Cipher Modes of Operation]]
