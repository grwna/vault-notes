Ahli forensik perlu paham sistem komputer yang beragam2.

Keyword
- **Volatile vs Non-volatile**
- **Booting**
	- Ketika boot ada menulis log
	- Mengikuti boot normal berpotensi menghilangkan barang bukti
	- Intercept boot normal
	- Power on -> POST -> Firmware (BIOS/UEFI)
	- Secure Boot dapat mengganggu proses forensil, namun bisa dimatikan
- **Forensic Boot Media**
	- PALADIN - Linux
	- WinFE - Windows
- **Physical Drive**
	- SSD
	- HDD
	- HPA & DCO - bagian pada hard drive yang tersembunyi
- **Skema Partisi**
	- MBR
	- GPT
- **Filesystem**
	- FAT -> file yang dihapus ditandai dengan xE5 (sigma character) pada direntry
	- Slack Space
	- NTFS -> $MFT (Master FIle Table) database entry-entry
	- Di NTFS tiap file ada dua timestamp (standard information dan file_name) File_name lebih sulit diubah
	- Resident vs Non-Resident -> Resident adalah file kecil yang data nnya disimpan langsung pada MFT
- **RAM**
	- Akuisisi harus pada *live system*, namun bisa mengubah isi RAM (*observer effect*)
	- 