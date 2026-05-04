## Intro
Basically [[Caesar Cipher]] but done using a key string. The shifts done to the plaintext is chosen according to the index of the alphabet of the current key character.

Example:
`Plaintext = "Hello"`
`Key = "iya"`

| $P_{i}$ | H   | e   | l   | l   | o   |
| ------- | --- | --- | --- | --- | --- |
| $K_{i}$ | i   | y   | a   | i   | y   |
| $Shift$ | 8   | 24  | 0   | 8   | 24  |
| $C_{i}$ | p   | c   | l   | t   | m   |
