# Generating a new GPG key

If you don't have an existing GPG key, you can generate a new GPG key to use for signing commits and tags.

## Platform navigation

- [Mac](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key?platform=mac)
- [Windows](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key?platform=windows)
- [Linux](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key?platform=linux)

### [Supported GPG key algorithms](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key#supported-gpg-key-algorithms)

GitHub supports several GPG key algorithms. If you try to add a key generated with an unsupported algorithm, you may encounter an error.

- RSA
- ElGamal
- DSA
- ECDH
- ECDSA
- EdDSA

## [Generating a GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key#generating-a-gpg-key)

**Note:** Before generating a new GPG key, make sure you've verified your email address. If you haven't verified your email address, you won't be able to sign commits and tags with GPG. For more information, see "[Verifying your email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/verifying-your-email-address)."

1. Download and install [the GPG command line tools](https://www.gnupg.org/download/) for your operating system. We generally recommend installing the latest version for your operating system.
2. Open Terminal.
3. Generate a GPG key pair. Since there are multiple versions of GPG, you may need to consult the relevant [_man page_](https://en.wikipedia.org/wiki/Man_page) to find the appropriate key generation command.
    - If you are on version 2.1.17 or greater, paste the text below to generate a GPG key pair.
        Shell

```bash
gpg --full-generate-key
```

- If you are not on version 2.1.17 or greater, the `gpg --full-generate-key` command doesn't work. Paste the text below and skip to step 6.
```bash    
gpg --default-new-key-algo rsa4096 --gen-key
```
  
- At the prompt, specify the kind of key you want, or press `Enter` to accept the default.  
- At the prompt, specify the key size you want, or press `Enter` to accept the default.
- Enter the length of time the key should be valid. Press `Enter` to specify the default selection, indicating that the key doesn't expire. Unless you require an expiration date, we recommend accepting this default.
- Verify that your selections are correct.
- Enter your user ID information.
    - **Note:** When asked to enter your email address, ensure that you enter the verified email address for your GitHub account. To keep your email address private, use your GitHub-provided `no-reply` email address. For more information, see "[Verifying your email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/verifying-your-email-address)" and "[Setting your commit email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address)." 
- Type a secure passphrase.
- Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
```bash
gpg --list-secret-keys --keyid-format=long
```

**Note:** Some GPG installations on Linux may require you to use `gpg2 --list-keys --keyid-format LONG` to view a list of your existing keys instead. In this case you will also need to configure Git to use `gpg2` by running `git config --global gpg.program gpg2`.
   
- From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```bash
gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot <hubot@example.com>
ssb   4096R/4BB6D45482678BE3 2016-03-10
```

2. Paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:
  
```bash
gpg --armor --export 3AA5C34371567BD2
# Prints the GPG key ID, in ASCII armor format
```

3. Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
4. [Add the GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account).

## [Further reading](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key#further-reading)

- "[Checking for existing GPG keys](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys)"
- "[Adding a GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)"
- "[Telling Git about your signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)"
- "[Associating an email with your GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/associating-an-email-with-your-gpg-key)"
- "[Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)"
- "[Signing tags](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-tags)"