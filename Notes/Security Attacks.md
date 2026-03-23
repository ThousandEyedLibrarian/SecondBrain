A security attack is any action that breaches or attempts to breach a security policy. Attacks split into two categories based on whether the system or data is altered.

### Passive Attacks

The attacker observes or monitors but **does not modify anything**. Hard to detect (no traces left), but easy to prevent (encrypt your traffic).

Two subtypes:
- **Release of message contents** - attacker captures and reads the actual data
- **Traffic analysis** - attacker can't read the data (it's encrypted) but observes patterns: who communicates with whom, how often, how much. Metadata alone is valuable intelligence

### Active Attacks

The attacker **modifies, disrupts, or fabricates** something. Hard to prevent, but easy to detect.

Four subtypes, each mapping to a security service they violate:
- **Interruption** - making resources unavailable. Violates *availability*. Classic example: DDoS.
- **Modification** - tampering with data in transit or at rest. Violates *integrity*. Example: man-in-the-middle altering transaction amounts.
- **Fabrication** - inserting fake data or impersonating an authorised user. Violates *integrity and authentication*. Example: phishing emails posing as a trusted entity.
- **Replay** - capturing legitimate data and retransmitting it later. The data is real and unmodified, but reused out of context. Countered by timestamps, sequence numbers, or nonces rather than encryption alone.

### Defensive asymmetry

The passive/active asymmetry shapes defensive strategy:
- For passive threats, focus on **prevention** (encryption)
- For active threats, focus on **detection and recovery** (audit trails, intrusion detection)

See also:
- [[CIA Triad]]
- [[Information Security]]
- [[Encryption]]
- [[Cryptography]]
