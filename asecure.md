# ASecure

An algorithm to encrypt data, and securing networking protocols.

# 1. Key Exchange

First, the two devices generate an RSA key (with 4096-bits length) and send their public keys. The device starting the connection must send first its public key, then the other device send its public key.

# 2. Symetric Key Exchange

First, the two devices generate an AES-256 key. Then, the device that started the connection sends its AES-256 key to the other device, encrypting it with the other device's public RSA key. And finally, the other device send its AES-256 key to the other device, encrypting it with the other device's public RSA key.

# 3. The Rest

Then, the devices can send data encrypted with the other device's AES-256 key.

# 4. Where this algorithm can be applied?

In whatever stream, already encrypted or not.