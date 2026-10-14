# Groups by Technique
## Substitution
## Transposition
- Columnar transposition
- Rail fence transposition
## Super-Encryption
A.K.A Product Cipher -> combines substitution and transposition

# Substitution Ciphers
## Monoalphabetic Cipher
One Pt letter to one Ct letter
- Caesar
## Polyalphabetic Cipher
One Pt letter can map to multiple Ct letter
- Vigenere
	- Full Vigenere (lookup table)
	- Auto-key (use plaintext as part of key)
	- Running-key (use long script text as key)
- Affine
	- Two keys: m (factor), b (shift)
	- C $\equiv$ mP + b (mod n)
	- P $\equiv$ $m^{-1}$(C - b) (mod n)

## Polygram Ciphers
- Playfair
	- 25 letters (no J)
	- Enkripsi: kanan -> bawah -> horizontal & vertikal
	- Dekripsi: kiri -> atas -> vertikal & horizontal
- Hill Cipher
	- Key: NxN matrix called $K$
	- Where N is the length of polygram
	- $C=KP$
	- $P=K^{-1}C$
	- Order of operations matter for matrix