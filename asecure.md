# ASecure

An algorithm to encrypt data, and securing networking protocols.

# 1. Key Exchange

First, the two devices generate an RSA key (with 4096-bits length) and send their public keys. The device starting the connection must send first its public key, then the other device send its public key. The RSA public key should be encoded with PKCS#1 and sent as bytes.
**Disclaimer**: All encryptions made with RSA keys should have PKCS#1v15 padding.

# 2. Symetric Key Exchange

First, the two devices generate an Salsa20-128 key. Then, the device that started the connection sends its Salsa20-128 key to the other device, encrypting it with the other device's public RSA key. And finally, the other device send its Salsa20-128 key to the other device, encrypting it with the other device's public RSA key.

# 3. The Rest

Then, the devices can send data encrypted with the other device's Salsa20-128 key. First send the nonce used encrypted with the other device's RSA key, then send the encrypted data.

# 4. Where this algorithm can be applied?

In whatever stream, already encrypted or not.