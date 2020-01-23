# PolySafe

Embed any file into an encrypted, self-decrypting HTML file.

## Features

* Encryption and decryption happen locally in the browser
* Encrypts arbitrary files (and their filename)
* Decryptor supports almost all browsers released 2015 or later

## Usage

### Encryption

1. Open a local or hosted copy of `polysafe.html` in your browser.
2. Select a file, enter a long and complex password and click `Encrypt`.
3. Store the encrypted, self-decrypting HTML file that will be downloaded.
4. (Optional) Rename the HTML file if you want to keep the filename secret.

### Decryption

1. Open the generated HTML file in your browser.
2. Enter the password and click `Decrypt`.
3. The original file with its original filename will be downloaded.

## Browser support

### Decryptor

* Firefox 34+ (Dec 2014)
* Chrome 38+, tested: 46+ (Oct 2015)
* Opera 29+ (Apr 2015)
* Safari 10.1+ untested and Desktop-only

### Encryptor

* Any recent version of Firefox, Chrome, Opera or (Desktop) Safari

## Security considerations

PolySafe relies on the following algorithms offered natively by the WebCrypto API and running directly in the browser:

* Authenticated encryption: AES-GCM (128 bits with a cryptographically random IV)
* Key derivation: PBKDF2 (200,000 rounds with a cryptographically random salt)

Combined with a high-entropy password, this algorithmic setup should be reasonably secure for most users and their data. However, not just because of the possibility of bugs and structural weaknesses in the implementation, **there can be no guarantee whatsoever for the confidentiality of the processed data**.

Note that PBKDF2 does **not** offer the same level of resistance against GPU- and ASIC-based attacks as more recent algorithms such as scrypt or Argon2. These algorithms are not supported by the WebCrypto API and would thus have made the implementation both more complex and much less efficient. Since "Never trust a random guy on GitHub" should come well before "Protect against dedicated adversaries with GPU clusters" in anyone's threat model, not supporting better key derivation algorithms is a trade-off I am willing to make.

Should the self-decrypting HTML file have passed outside of your control between creating it and decrypting it again (e.g. you sent it to yourself by email or uploaded it somewhere on the web), then you may want to verify that the file has not been tampered with. For example the file could have been modified in such a way that the password will be leaked.

## License

MIT
