*This is a guide that is designed to be maximally efficient for quick set up and use... If you are looking for further details on this topic, please reach out to me via email at kyle@archn3m3sis.com

## Step 01 - Generating An RSA Key Pair From The Command Line 

---
```bash
ssh-keygen -o -t rsa -C "Github Auhtentication Key | Contact >>> [kyle@archn3m3sis.com] With Any Issues Or Auth Errors"
```
- [f] The `-O` represents the 'options' arguments for the sshkeygen command
- [f] The `-t` represents the type of key that we will be creating (in this case we will be generating an `rsa` key)
- [f] The `-C` option represents that we will be inserting a comment following this input (in our case it is an email comment for our key [kyle@archn3m3sis.com] 

```bash
cat /home/archn3m3sis/.ssh/Github-SSH-Sessions/id_rsa.pub
```

## Step 02 - Copy The Output From `cat` To Your Github Account 
1) Go online to Github.com and click on your profile...
    - go to your **settings**... 
        - in your submenu go to **developer settings**...
            - You should see a categorical menu for 'SSH and GPG Keys' | This is where you want to end up...
2) Under The 'SSH Keys' header, click on `new SSH key`...
3) Paster the SSH key you copied from the output of your cat command in the previous step into the text entry box displayed within Github...
4) Save your changes and authenticate with 2 Factor for Github... 
















## Optional In Depth Reading For `SSH Related Tools & Commands`
- [ssh-keygen](https://www.ssh.com/ssh/keygen) - creates a key pair for public key authentication
    
- [ssh-copy-id](https://www.ssh.com/ssh/copy-id) - configures a public key as authorized on a server
    
- [ssh-agent](https://www.ssh.com/ssh/agent) - agent to hold private key for single sign-on
    
- [ssh-add](https://www.ssh.com/ssh/add) - tool to add a key to the agent
    
- [scp](https://www.ssh.com/ssh/scp) - file transfer client with RCP-like command interface
    
- [sftp](https://www.ssh.com/ssh/sftp) - file transfer client with FTP-like command interface
    
- [sshd](https://www.ssh.com/ssh/sshd) - OpenSSH server

## Command & Option Summary For `openssh`

**-1** Use protocol version 1 only.
**-2** Use protocol version 2 only.
**-4** Use IPv4 addresses only.
**-6** Use IPv6 addresses only.
**-A** Enable forwarding of the authentication agent connection.
**-a** Disable forwarding of the authentication agent connection.
**-C** Use data compression
**-c cipher_spec** Selects the cipher specification for encrypting the session.
**-D** `**[bind_address:]**`**port** Dynamic application-level port forwarding. This allocates a socket to listen to port on the local side. When a connection is made to this port, the connection is forwarded over the secure channel, and the application protocol is then used to determine where to connect to from the remote machine.
**-E log_file** Append debug logs to log_file instead of standard error.
**-F configfile** Specifies a per-user configuration file. The default for the per-user configuration file is ~/.ssh/config.
**-g** Allows remote hosts to connect to local forwarded ports.
**-i identity_file** A file from which the [identity key](https://www.ssh.com/ssh/identity-key) (private key) for [public key authentication](https://www.ssh.com/ssh/public-key-authentication) is read.
**-J** `**[user@]**`**host**`**[:port]**` Connect to the target host by first making a ssh connection to the pjump host[(/iam/jump-host) and then establishing a [TCP forwarding](https://www.ssh.com/ssh/tunneling/example) to the ultimate destination from there.
**-l login_name** Specifies the user to log in as on the remote machine.
**-p port** Port to connect to on the remote host.
**-q** Quiet mode.
**-V** Display the version number.
**-v** Verbose mode.
**-X** Enables X11 forwarding.

## Command and Option Summary For `ssh-keygen`

**Here's a summary of commonly used options to the keygen tool:**

**-b** “Bits” This option specifies the number of bits in the key. The regulations that govern the use case for SSH may require a specific key length to be used. In general, 2048 bits is considered to be sufficient for RSA keys.
**-e** “Export” This option allows reformatting of existing keys between the OpenSSH key file format and the format documented in [RFC 4716](https://tools.ietf.org/html/rfc4716), “SSH Public Key File Format”.
**-p** “Change the passphrase” This option allows changing the passphrase of a private key file with `**[-P old_passphrase]**` and `**[-N new_passphrase]**`, `**[-f keyfile]**`.
**-t** “Type” This option specifies the type of key to be created. Commonly used values are: **- rsa** for [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) keys **- dsa** for [DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm) keys **- ecdsa** for [elliptic curve DSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) keys
**-i** "Input" When _ssh-keygen_ is required to access an existing key, this option designates the file.
**-f** "File" Specifies name of the file in which to store the created key.
**-N** "New" Provides a new passphrase for the key.
**-P** "Passphrase" Provides the (old) passphrase when reading a key.
**-c** "Comment" Changes the comment for a keyfile.
**-p** Change the passphrase of a private key file.
**-q** Silence ssh-keygen.
**-v** Verbose mode.
**-l** "Fingerprint" Print the fingerprint of the specified public key.
**-B** "Bubble babble" Shows a "bubble babble" (Tectia format) fingerprint of a keyfile.
**-F** Search for a specified hostname in a known_hosts file.
**-R** Remove all keys belonging to a hostname from a known_hosts file.
**-y** Read a private OpenSSH format file and print an OpenSSH public key to stdout.

*This only listed the most commonly used options. For full usage, including the more exotic and special-purpose options, use the `man ssh-keygen` command.*

```bash
man ssh-keygen
```

