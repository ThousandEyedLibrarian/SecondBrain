The three primary security objectives underpinning [[Information Security]]. Every security discussion comes back to these.

### Confidentiality

Information is not disclosed to unauthorised entities. **Confidentiality breaches are irreversible** - once a secret is out, you can't un-reveal it. This is what makes it different from the other two: integrity and availability can be restored, confidentiality cannot.

Primary mechanism: [[Encryption]].

### Integrity

Data has not been modified in an unauthorised or undetected way. Covers accuracy, completeness, and consistency of data over its entire lifecycle.

Mechanisms: message authentication codes (MAC), authenticated encryption, digital signatures.

### Availability

Resources are accessible and usable when legitimate users need them. High availability systems aim to prevent disruption from power outages, hardware failures, and system upgrades.

### The Tension

These three properties often pull against each other. Maximising confidentiality (lock everything down, minimise copies) tends to hurt availability. Maximising availability (replicate everywhere, open access) tends to hurt confidentiality. Security design is about finding the right balance for the context.

### Extended Security Services

Beyond the triad, three additional services:
- **Authentication** - verifying identity. Three factor types: something you *know* (password), something you *have* (card), something you *are* (biometrics). Multi-factor is stronger than single-factor because different factor types require completely independent attack vectors.
- **Non-repudiation** - proof that someone did something, preventing them from denying it after the fact. Provided by digital signatures.
- **Access control** - restricting what authenticated users can actually do. Authentication says who you are, access control says what you're allowed to touch.

These chain together: authentication -> access control -> non-repudiation.

See also:
- [[Information Security]]
- [[Cryptography]]
- [[Encryption]]
