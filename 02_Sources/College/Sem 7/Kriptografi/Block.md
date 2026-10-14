# Modes of Operations
- ECB
	- E(P, K)
		- parallelizable
		- isolated error
- CBC
	- FB = feedback (at first, FB = IV/Nonce)
	- E(K, FB $\oplus$ P)
	- C = E 
	- Cipher is chained forward
	- Benefits/drawbacks
		- error is propagated on encryption
**Stream-like**
Stream like because the encryption is actually keystream generation. Then plaintext blocks are xored using this keystream.
- CFB
	- E(FB, K)
	- C = E $\oplus$ P
	- C is chained forward
	- Error is propagated on encryption
- OFB
	- E(FB, K)
	- C = E $\oplus$ P
	- E is chained forward (output)
	- Error is not propagated
- CTR
	- Much like OFB, but nothing is chained forward
	- FB is replaced with a counter value
	- Parallelizable
NOTE: 
for the stream-like, encryption and decryption is the exact same process, with the difference being the position of ciphertext and plaintext. 
This is important because in CBC , the ciphertext is chained forward in encrypt and decrypt. For stream-likes (specifically CFB), plaintext is chained forward in decryption but ciphertext is chained for encryption

**Feistel**
- Ri = L[i-1] $\oplus$ f(R[i-1])

# Some Block Ciphers
## DES

## Triple DES

## AES

## Other
- GOST
- RC5
- RC6