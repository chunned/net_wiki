[Source](https://tryhackme.com/r/room/ccstego)

## Steghide
Steghide is used to hide information in JPGs (note that it *only* works on JPGs). Install with `apt install steghide`.
**Flags**
- `embed` or `--embed`: embeds secret data in a cover file
- `-ef` or `--embedfile`: specify file to embed data to
- `-cf` or `--coverfile`: specify cover file (must be one of the following formats: AU, BMP, JPEG, WAV)
	- `-p`: specify passphrase to use for the cover file
- `-sf` or `--stegofile`: specify the name for the stego file that will be created from the operation
- `extract`: extract data from a file
	- `-sf` or `--stegofile`: specify name of file to extract from

## Zsteg
Equivalent to Steghide, but for PNG and BMP. Install with `gem install zsteg`.
- `--lsb`: Least significant bit comes first
- `--msb`: Most significant bit comes first
- `-E <name>`: extract specified payload

## Exiftool
Technically not a steganography tool, but useful for viewing metadata of images.
`apt install exiftool`

## Stegoveritas
Supports most image file formats. Contains many built in tests to extract data, which is useful if you're not sure what you're looking for.
`pip3 install stegoveritas`, `stegoveritas_install_deps`
- `-meta`: check file for metadata info
- `-steghide`: check steghide for hidden info
- `-extractLSB`: extract a specific LSB RGB from the image; used with `-red`, `-green`, `-blue`, `-alpha`

## Spectrograms
Use SonicVisualizer. Import file, go Layer > Add Spectrogram

## QR Codes
Use zbar - `sudo apt install zbar-tools`
`zbarimg <file>`