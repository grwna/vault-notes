# Steganography
- Embedded message (hiddentext)
- Cover-object/Covertext
- Stego-object
- Stego-key

**Criteria**
- Imperceptible
- Fidelity
- Recovery
- Capacity

**LSB Methods Variants**
- Sequential
- Random -> uses stego-key
- m-bit LSB -> not just least but also 2nd least, etc.
- Encryption

**NoStega**
- GraphStega -> plot message to graph
- Chess-stega
- Header-stega
- 
# Steganalysis
**Types**
- Targeted -> specific technique on specific file formats
- Blind

**Methods**
- Visual attacks
	- LSB plane attack
	- Filtered visual attack
- Statistical attacks
	- Histogram analysis
	- Regular-singular analysis
	- Chi-square analysis
	- Sample pair analysis

# Digital Watermarking
**Classifications**
- Paper watermarking
- Digital watermarking

**Invisible Watermarking**
- Fragile watermarking - integrity
	- Broken watermark is a tell
	- Uses LSB steganography
- Robust watermarking - ownership labeling
	- We don't want watermark to be broken
	- So editing and other manipulation still shows the watermark
	- Uses advanced algorithm

**Applications**
- Owner identification
- Proof of ownership
- Tamper proofing
- Transaction tracking
- Piracy protection
- Broadcast monitoring

**Digital Rights Management**