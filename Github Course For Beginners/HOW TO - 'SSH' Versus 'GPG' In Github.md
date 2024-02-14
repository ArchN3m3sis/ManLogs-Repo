- [W] **Generating a GPG signing key is more involved than generating an SSH key, but GPG has features that SSH does not**. A GPG key can expire or be revoked when no longer used. GitHub shows commits that were signed with such a key as "Verified" unless the key was marked as compromised. SSH keys don't have this capability.

## [GPG commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification#gpg-commit-signature-verification)

You can use GPG to sign commits with a GPG key that you generate yourself.

GitHub uses OpenPGP libraries to confirm that your locally signed commits and tags are cryptographically verifiable against a public key you have added to your account on GitHub.com.

To sign commits using GPG and have those commits verified on GitHub, follow these steps:

1. [Check for existing GPG keys](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys)
2. [Generate a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
3. [Add a GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)
4. [Tell Git about your signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)
5. [Sign commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)
6. [Sign tags](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-tags)

### [Supported GPG Key Algorithms](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys#supported-gpg-key-algorithms)

*GitHub supports several GPG key algorithms. If you try to add a key generated with an unsupported algorithm, you may encounter an error.*

- RSA
- ElGamal
- DSA
- ECDH
- ECDSA
- EdDSA

#### Step 01 - Verifying Current GPG Keys On Your System 
**Note:** GPG does not come installed by default on macOS or Windows. To install GPG command line tools, see [GnuPG's Download page](https://www.gnupg.org/download/).

1. Open Terminal.
2. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
             Shell

```shell
gpg --list-secret-keys --keyid-format=long
```

**Note:** Some GPG installations on Linux may require you to use `gpg2 --list-keys --keyid-format LONG` to view a list of your existing keys instead. In this case you will also need to configure Git to use `gpg2` by running `git config --global gpg.program gpg2`.

- Check the command output to see if you have a GPG key pair.
    - If there are no GPG key pairs or you don't want to use any that are available for signing commits and tags, then [generate a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key).
    - If there's an existing GPG key pair and you want to use it to sign commits and tags, you can display the public key using the following command, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

        ```shell
        $ gpg --armor --export 3AA5C34371567BD2
        # Prints the GPG key ID, in ASCII armor format
        ```

        You can then [add your GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account).

# Adding a GPG key to your GitHub account

- [i] To sign commits associated with your account on GitHub, you can add a public GPG key to your personal account. Before you add a key, you should check for existing keys. If you don't find any existing keys, you can generate and copy a new key. For more information, see "[Checking for existing GPG keys](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys)" and "[Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)."

- [i] You can add multiple public keys to your account on GitHub. Commits signed by any of the corresponding private keys will show as verified. If you remove a public key, any commits signed by the corresponding private key will no longer show as verified.

- [i] To verify as many of your commits as possible, you can add expired and revoked keys. If the key meets all other verification requirements, commits that were previously signed by any of the corresponding private keys will show as verified and indicate that their signing key is expired or revoked.

![Screenshot of a list of commits. One commit is marked with a "Verified" label. Below the label, a dropdown explains that the commit was signed, but the key has now expired.](https://docs.github.com/assets/cb-97945/images/help/settings/gpg-verified-with-expired-key.png)

### [Supported GPG key algorithms](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account#supported-gpg-key-algorithms)

GitHub supports several GPG key algorithms. If you try to add a key generated with an unsupported algorithm, you may encounter an error.

- RSA
- ElGamal
- DSA
- ECDH
- ECDSA
- EdDSA

When verifying a signature, GitHub extracts the signature and attempts to parse its key ID. The key ID is then matched with keys added to GitHub. Until a matching GPG key is added to GitHub, it cannot verify your signatures.

## [Adding a GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account#adding-a-gpg-key)

1. In the upper-right corner of any page, click your profile photo, then click **Settings**.
    ![Screenshot of a user's account menu on GitHub. The menu item "Settings" is outlined in dark orange.](https://docs.github.com/assets/cb-45016/images/help/settings/userbar-account-settings-global-nav-update.png)
2. In the "Access" section of the sidebar, click
1. **SSH and GPG keys**.
2. Next to the "GPG keys" header, click **New GPG key**.
3. In the "Title" field, type a name for your GPG key.
4. In the "Key" field, paste the GPG key you copied when you [generated your GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key).
5. Click **Add GPG key**.
6. To confirm the action, authenticate to your GitHub account.

## [Further reading](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account#further-reading)

---
- "[Checking for existing GPG keys](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys)"
- "[Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)"
- "[Telling Git about your signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)"
- "[Associating an email with your GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/associating-an-email-with-your-gpg-key)"
- "[Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)"
- "[About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)"

# Telling Git about your signing key

---
To sign commits locally, you need to inform Git that there's a GPG, SSH, or X.509 key you'd like to use.


## [Telling Git about your GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-gpg-key)

If you're using a GPG key that matches your committer identity and your verified email address associated with your account on GitHub.com, then you can begin signing commits and signing tags.

If you don't have a GPG key that matches your committer identity, you need to associate an email with an existing key. For more information, see "[Associating an email with your GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/associating-an-email-with-your-gpg-key)".

If you have multiple GPG keys, you need to tell Git which one to use.

1. Open Terminal.
2. If you have previously configured Git to use a different key format when signing with `--gpg-sign`, unset this configuration so the default format of `openpgp` will be used.
    
    ```shell
    git config --global --unset gpg.format
    ```
    
3. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
    
    Shell
    

- ```shell
    gpg --list-secret-keys --keyid-format=long
    ```
    
    **Note:** Some GPG installations on Linux may require you to use `gpg2 --list-keys --keyid-format LONG` to view a list of your existing keys instead. In this case you will also need to configure Git to use `gpg2` by running `git config --global gpg.program gpg2`.
    
- From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:
    
    Shell
    

1. ```shell
    
    $ gpg --list-secret-keys --keyid-format=long
    /Users/hubot/.gnupg/secring.gpg
    ------------------------------------
    sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
    uid                          Hubot <hubot@example.com>
    ssb   4096R/4BB6D45482678BE3 2016-03-10
    ```
    
2. To set your primary GPG signing key in Git, paste the text below, substituting in the GPG primary key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:
    
    ```shell
    git config --global user.signingkey 3AA5C34371567BD2
    ```
    
    Alternatively, when setting a subkey include the `!` suffix. In this example, the GPG subkey ID is `4BB6D45482678BE3`:
    
    ```shell
    git config --global user.signingkey 4BB6D45482678BE3!
    ```
    
3. Optionally, to configure Git to sign all commits by default, enter the following command:
    
    ```shell
    git config --global commit.gpgsign true
    ```
    
    For more information, see "[Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)."
    
4. To add your GPG key to your `.bashrc` startup file, run the following command:
    
    ```bash
    [ -f ~/.bashrc ] && echo -e '\nexport GPG_TTY=$(tty)' >> ~/.bashrc
    ```
    

## [Telling Git about your SSH key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key)

You can use an existing SSH key to sign commits and tags, or generate a new one specifically for signing. For more information, see "[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)."

**Note:** SSH signature verification is available in Git 2.34 or later. To update your version of Git, see the [Git](https://git-scm.com/downloads) website.

1. Open Terminal.
    
2. Configure Git to use SSH to sign commits and tags:
    
    ```bash
    git config --global gpg.format ssh
    ```
    
3. To set your SSH signing key in Git, paste the text below, substituting **/PATH/TO/.SSH/KEY.PUB** with the path to the public key you'd like to use.
    
    ```bash
    git config --global user.signingkey /PATH/TO/.SSH/KEY.PUB
    ```
    

## [Telling Git about your X.509 key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-x509-key)

You can use [smimesign](https://github.com/github/smimesign) to sign commits and tags using S/MIME.

**Note:** S/MIME signature verification is available in Git 2.19 or later. To update your version of Git, see the [Git](https://git-scm.com/downloads) website.

1. Install [smimesign](https://github.com/github/smimesign#installation).
    
2. Open Terminal.
    
3. Configure Git to use S/MIME to sign commits and tags. In Git 2.19 or later, use the `git config gpg.x509.program` and `git config gpg.format` commands:
    
    - To use S/MIME to sign for all repositories:
        
        ```shell
        git config --global gpg.x509.program smimesign
        git config --global gpg.format x509
        ```
        
    - To use S/MIME to sign for a single repository:
        
        ```shell
        cd PATH-TO-REPOSITORY
        git config --local gpg.x509.program smimesign
        git config --local gpg.format x509
        ```
        
        In Git 2.18 or earlier, use the `git config gpg.program` command:
        
    - To use S/MIME to sign for all repositories:
        
        ```shell
        git config --global gpg.program smimesign
        ```
        
    - To use S/MIME to sign for a single repository:
        
        ```shell
        cd  PATH-TO-REPOSITORY
        git config --local gpg.program smimesign
        ```
        
        If you're using an X.509 key that matches your committer identity, you can begin signing commits and tags.
        
4. If you're not using an X.509 key that matches your committer identity, list X.509 keys for which you have both a certificate and private key using the `smimesign --list-keys` command.
    
    ```shell
    smimesign --list-keys
    ```
    
5. From the list of X.509 keys, copy the certificate ID of the X.509 key you'd like to use. In this example, the certificate ID is `0ff455a2708394633e4bb2f88002e3cd80cbd76f`:
    
    ```shell
    $ smimesign --list-keys
                 ID: 0ff455a2708394633e4bb2f88002e3cd80cbd76f
                S/N: a2dfa7e8c9c4d1616f1009c988bb70f
          Algorithm: SHA256-RSA
           Validity: 2017-11-22 00:00:00 +0000 UTC - 2020-11-22 12:00:00 +0000 UTC
             Issuer: CN=DigiCert SHA2 Assured ID CA,OU=www.digicert.com,O=DigiCert Inc,C=US
            Subject: CN=Octocat,O=GitHub\, Inc.,L=San Francisco,ST=California,C=US
             Emails: octocat@github.com
    ```
    
6. To set your X.509 signing key in Git, paste the text below, substituting in the certificate ID you copied earlier.
    
    - To use your X.509 key to sign for all repositories:
        
        ```shell
        git config --global user.signingkey 0ff455a2708394633e4bb2f88002e3cd80cbd76f
        ```
        
    - To use your X.509 key to sign for a single repository:
        
        ```shell
        cd  PATH-TO-REPOSITORY
        git config --local user.signingkey 0ff455a2708394633e4bb2f88002e3cd80cbd76f
        ```
## [SSH commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification#ssh-commit-signature-verification)

You can use SSH to sign commits with an SSH key that you generate yourself. For more information, see the [Git reference documentation](https://git-scm.com/docs/git-config#Documentation/git-config.txt-usersigningKey) for `user.Signingkey`. If you already use an SSH key to authenticate with GitHub, you can also upload that same key again for use as a signing key. There's no limit on the number of signing keys you can add to your account.

GitHub uses [ssh_data](https://github.com/github/ssh_data), an open source Ruby library, to confirm that your locally signed commits and tags are cryptographically verifiable against a public key you have added to your account on GitHub.com.

**Note:** SSH signature verification is available in Git 2.34 or later. To update your version of Git, see the [Git](https://git-scm.com/downloads) website.

To sign commits using SSH and have those commits verified on GitHub, follow these steps:

1. [Check for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
2. [Generate a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
3. [Add a SSH signing key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
4. [Tell Git about your signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)
5. [Sign commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)
6. [Sign tags](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-tags)





