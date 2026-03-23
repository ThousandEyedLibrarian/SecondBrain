The practice of preventing and detecting attacks on information-based systems. Not just about keeping attackers out - detection matters equally because some attacks (particularly passive ones) can't always be prevented.

Three core concerns:
- **Security attacks/threats** - ways a security policy might be breached
- **Security services** - measures to counter those threats (see [[CIA Triad]])
- **Security mechanisms** - the actual tools and techniques that deliver those services (e.g. [[Encryption]], digital signatures, access control lists)

### Security Standards

Formal specifications for how to protect cyber environments. Notable examples:
- **ISO/IEC 27000 series** - Australia's standard of choice
- **ITU-T X.800** - OSI security architecture, provides the conceptual framework used broadly in the field
- **NIST FIPS** - US national standard (AES is defined here)

### Model for Network Security

Any secure communication system needs to solve four problems:
1. Design the security algorithm (encryption scheme, hash function, etc.)
2. Generate the secret information (keys)
3. Distribute and share those keys securely - this is famously the hardest part
4. Define a protocol tying it all together

A weakness at any layer breaks the whole system. Key distribution in particular is the problem that much of [[Cryptography]] exists to solve.

There's a separate model for **network access security** which is about controlling who gets into a system in the first place (gatekeepers, firewalls, login systems) rather than protecting data in transit.

See also:
- [[CIA Triad]]
- [[Cryptography]]
- [[Cybersecurity]]
- [[Application Security]]
