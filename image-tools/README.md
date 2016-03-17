# Image Tools

This folder contains tools for generating unencrypted and encrypted firmware update images.

## Requirements

Python 3.x

## Genimage

The genimage.py script generates unencrypted firmware update images.  The script requires an Intel HEX file as input and outputs a binary file.  Genimage.py will attempt to automatically determine the start address of the application.  However, it can also be specified directly on the command line.  See README.md in the genimage folder for more information on the usage of this tool.  Genimage can also be used to generate firmware package updates for the Bootloader and SoftDevice but this usage is not recommended for production product.

## Signimage

The Signimage tool is a C++ program compiled against the Crypto++ library.  The only use of this tool is to encrypt firmware update images using AES 128-bit EAX mode.  Different executables for the various system types are provided.  At preset, the program is built for Linux, OS X, and Windows 64-bit and 32-bit systems.  If another system is needed, please contact Rigado to get the source for this tool.

Signimage takes in an unencrypted firmware update image and the private key.  The program outputs an encrypted binary with the appropriate information for the bootloader.  

> Generating images with a key of all 0s or Fs will NOT produce a valid image for the unencrypted bootloader.  If using the unencrypted bootloader, signimage is not used.

### Linux

```
usage: ./signimage-linux <input.bin> <output.bin> <key>
  <input.bin> must be an unencrypted image, as generated by genimage
  <key> is 32 hex characters, e.g.: 00112233445566778899aabbccddeeff
```

### OS X

```
usage: ./signimage-osx <input.bin> <output.bin> <key>
  <input.bin> must be an unencrypted image, as generated by genimage
  <key> is 32 hex characters, e.g.: 00112233445566778899aabbccddeeff
```

### Windows 64-bit Usage

```
usage: signimage-w64.exe <input.bin> <output.bin> <key>
  <input.bin> must be an unencrypted image, as generated by genimage
  <key> is 32 hex characters, e.g.: 00112233445566778899aabbccddeeff
```

### Windows 32-bit Usage

```
usage: signimage-w32.exe <input.bin> <output.bin> <key>
  <input.bin> must be an unencrypted image, as generated by genimage
  <key> is 32 hex characters, e.g.: 00112233445566778899aabbccddeeff
```