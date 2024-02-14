

## Access Tokens

```
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
```

- [!] *The access token above is for my Zephyrus local authentication*



## GPG keys

- [@] 

>[!Important] See The Following In Regard To Github GPG Keys
==Managing commit signature verification== >>> GitHub will verify GPG, SSH, or S/MIME signatures so other people will know that your commits come from a trusted source. GitHub will automatically sign commits you make using the GitHub web interface.


## SSH Keys 

- [&] Github Authentication SSH Key For ROG Zephyrus Local Sessions

*Step 01* - *Generating The SSH Key-Pair*

- [i] If you want to SSH into github, then you will need the proper SSH keys... The first thing to do is to ensure that you have SSH enabled within your local machine... 

- [i] To generate the SSH Key-Pair, then simply follow the code listed below: 

**Input For Terminal**
```bash
ssh-keygen -o -t rsa -C "kyle@archn3m3sis.com"
```
**Output From Terminal**
```bash
The key fingerprint is:
SHA256:sz04Ki7saYgEuirocyN7XhE/+eMFy6hyAaXyuEnaytA kyle@archn3m3sis.com
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|     .           |
|    o.           |
|.. o  o .        |
|o + .. +S.       |
|.= . .. ==o      |
|B=E  ...+=o.     |
|X==*o.....o.     |
|*BX+=o.  .       |
+----[SHA256]-----+


- You will be prompted to select a file for the key pair. ==The default directory for SSH keys is== >>> ==`~/.ssh`== with *the private key named `id_rsa` and the public key named `id_rsa.pub`*. By using the default file names, the SSH client will be able to automatically locate the keys during authentication so it is strongly recommended to not change them. You can use the default by pressing the Enter key.
```

- After you have selected the file for the key pair, you be will be prompted to enter a passphrase to encrypt private key file. Encrypting the private key with a passphrase is _optional_, but it will improve security the keys. If you enter a passphrase you will have to provide each it time you use the key. You can press the Enter key to not use a passphrase; we strongly recommend the use of a passphrase with SSH keys.


# Uploading Keys Via Command Line

- If you currently have access to SSH on your server, you can upload the key over the command line.

- Retrieve the contents of the public key. If the key was created in the default location, this can be done by outputting the contents of `~/.ssh/id_rsa.pub`.

```bash
cat ~/.ssh/id_rsa.pub
```

- The output will look similar to the following:

```bash
ssh-rsa AAAAB9NzaC1yc2EAAAADAQABAAABAQDBej/3XAjhwTwWXsOJmDdKTLtjnpGXsHOAEIYC12qQ r51+AVJPNsqcDlFdv+Lr/XufQDCh2gXz+ieA/LJNb5luxReaVVbKtvAONZgv8uLD1J8kzRXike3h9L53 oIo2j8Lt4fuzB8yAWkwBelurn4OWfk0K6gFXN86RgprKSPN3GbwG6MINAor7NwCHzJhVK9u6Jpw9EPJv Dl4co+N9L+CGgudvY7iBNzIofE9MP68lXcql4bMWz3+2H0FWKHZ1rSJz56KjoCKBPWTqdFq5o1AIcauc ECgiTaEGcSNk4+T0A8BuAOd3a4O9Gr6y8C4Sn4ghYajJVWsszP2B1tTGAc3L
```

- Open the (and create if it doesn't exist) `~/.ssh/authorized_keys` file using a text editor such as `nano`, `pico`, or `vim`.

```bash
nano ~/.ssh/authorized_keys
```

- [!] If you had to create the `~/.ssh/` directory, or the `authorized_keys` file, you need to verify the permissions are correct, or you won't be able to login.

```bash
chmod 700 ~/.shh
chmod 600 ~/.ssh/authorized_keys
```

- Paste the public key at the bottom of the file, and then save and close the file.

- [R] Alternatively, you can append the public key to `~/.ssh/authorized_keys` with a single command.

- [W] You can use the `cat` command if the public key is stored in a file.

```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

- If the public key is not stored as a file on the server, you can use the `echo` command.

```bash
echo "ssh-rsa AAAAB9N...sszP2B1tTGAc3L" >> ~/.ssh/authorized_keys
```

- [!] Be sure to include the entire public key in quotes after `echo`.

- Once the public key is added to the `authorized_keys` file, you should be able to login using your SSH keys.
















