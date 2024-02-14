Your keys are stored in **a directory called ".** **gnupg" in your home directory**. This directory will also store the public keys of anyone that has sent encrypted files to you. When you import their public keys, they are added to an indexed database file in that directory.



```tree-gnupg
.gnupg
├── openpgp-revocs.d
│   ├── 3EA76F81703FD44360298AC1C09A29F1F4835B19.rev
│   └── E5060153A51C7EFA2FC010E5B412B9D49A6BD4E7.rev
├── private-keys-v1.d
│   ├── 5E35778CF64E4F74D164666D7939447DB3CB347E.key
│   └── EAF5BA893143C4E79AD2599D046B5CA1E880C93B.key
├── pubring.kbx
├── pubring.kbx~
├── sshcontrol
├── tofu.db
└── trustdb.gpg

2 directories, 9 files
```

The contents of the directory tree are:

- **openpgp-revocs.d**: This subdirectory contains your revocation certificate. You'll need this if your private key ever becomes common knowledge or otherwise compromised. Your revocation certificate is used in the process of retiring your old keys and adopting new keys.
- **private-keys-v1.d**: This subdirectory stores your private keys.
- **pubring.kbx**: An encrypted file. It contains public keys, including yours, and some metadata about them.
- **pubring.kbx~**: This is a backup copy of "pubring.kbx." It is updated just before changes are made to "pubring.kbx."
- **trustdb.gpg**: This holds the trust relationships you have established for your own keys and for any accepted public keys belonging to other people.

- [R] You should be making regular, frequent backups of your home directory anyway, including the hidden files and folders. That will back up the ".gnupg" directory as a matter of course.

- [R] But you may think that your GPG keys are important enough to warrant a periodic backup of their own, or perhaps you want to copy your keys from your desktop to your laptop so that you have them on both machines. You're you on both machines, after all.


