The historical ciphers that predate modern [[Cryptography]]. Not used in practice anymore, but understanding why each one fails explains why modern ciphers are built the way they are.

### Substitution Ciphers

Replace symbols with other symbols. The progression of substitution ciphers is a story of trying (and failing) to hide letter frequency distributions.

**Caesar cipher** - shift every letter by a fixed amount. `C = (P + k) mod 26`. Only 25 usable keys, trivially brute-forced.

**Monoalphabetic cipher** - map each letter to a random different letter (1-to-1 mapping). Key space jumps to 26! (over 4 x 10^26), making brute force impractical. But each plaintext letter always maps to the same ciphertext letter, so frequency analysis cracks it - the most common ciphertext letter is probably 'e'. Al-Kindi described this attack in the 9th century.

**Polyalphabetic ciphers (Vigenere)** - use a repeating keyword where each letter determines a different Caesar shift. The same plaintext letter can produce different ciphertext letters depending on position, which flattens frequency distributions. Broken by the Kasiski method: find repeated sequences in the ciphertext, measure distances between them, and the common divisor of those distances gives the keyword length. Then attack each position group as a separate Caesar cipher.

**Autokey cipher** - uses the keyword followed by the plaintext itself as the key. Key never repeats, but since the plaintext is natural language the key inherits its frequency characteristics.

**One-time pad** - truly random key as long as the message, used only once. Shannon proved this gives perfect secrecy (ciphertext has zero statistical relationship to plaintext). Impractical because: keys must be as long as messages, must be truly random, must be securely distributed, and can never be reused.

### Transposition Ciphers

Keep the original symbols but rearrange their positions. The frequency distribution is identical to the plaintext, so these are vulnerable to different analysis techniques.

**Rail fence** - write message in a zigzag across n rows, read off row by row.

**Row transposition** - write message into a grid, read columns in an order determined by the key.

### Product Ciphers

Neither substitution nor transposition alone is secure. Stacking multiple of the same type doesn't help much either. But substitution followed by transposition combines both effects and is much harder to break. This is the bridge to modern ciphers - [[AES]] is essentially many rounds of substitution and transposition layered together.

See also:
- [[Cryptography]]
- [[Encryption]]
- [[AES]]
