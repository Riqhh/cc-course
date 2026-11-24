# H5 - Alice and Bob

## Read and summarize

### Terminology

* Message is plaintext or cleartext and encryption is process for turning it to ciphertext. To turn it back to plaintext decryption is used.
* Authentication for verifying message origin
* Integrity verify that message has not been modified in transit
* Nonrepudiation for sender can't deny that he sent the message
* Cryptographic algorithm (cipher) is mathematical function used to encryption and decryption
* Many cryptographuc algorithm uses a key with encryption and decryptions. Algorithm can use different key for encryption and decryption.
* Symmetric algorithm where encryption key can be calculated from decryption key and vice versa.
* Asymmetric algorithm or Public-Key Algorithm where public key can be used to encrypt, and private key to decrypt. Public key can be shared

### Communication using public-key cryptography

* Protocol is series of steps all needed to complete in order from start to finish. Protocol requires atleast two parties who know the protocol for example Alice and Bob.
* In public-key cryptography Bob sends Alice his public key and Alice encrypts her message using Bob's public key and sends it to Bob. Bob decrypts Alice's message using his private key
* Public-key algorithms are not used to encrypt data, they are used to encrypt keys. There are two main reasons: public-key algorithms are slow, and vulnerable to chosen-plaintext attacks.
* Hybrid cryptosystem refers to public-key cryptography where it's used to secure and distribute session keys used with symmetric algorithms
* Merkle's puzzles let two people create a shared secret key over an insecure connection. An attacker has to do much more work to discover the same key.

## Part A - Public key today

Tick-tock

## Part B - Encrypting and decrypting a message

Tick-tock

## Part C - Password management

I decided to try KeePassDroid, a password manager for Android based on the KeePass desktop application, which is available for Windows, Linux, and Mac. Both support kdbx -database files, although using the same database on multiple devices can be inconvenient. One suggested solution is to synchronize the database using a service such as Dropbox.

The password database can be protected with a master password, a key file, or a combination of both. It is also possible to choose which encryption algorithms are used.

### When not using password manager

When attacking against people not using password managers, the attack usually exploit weak or reused passwords. Password managers make it easy to use different and long random password for every service.

* Short rememreable password are more likely vulnerable to brute-force attacks
* Password leaked from one service can be reused to try logging into other services
* Manually typed password can be more likely to tricked entering then on fake login. Password managers usually autofill credentials only to regogniced services. 
