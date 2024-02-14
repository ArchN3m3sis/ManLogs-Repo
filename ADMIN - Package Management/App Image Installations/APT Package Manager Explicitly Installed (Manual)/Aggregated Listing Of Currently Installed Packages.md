```bash
sudo apt install apparmor apparmor-profiles apparmor-utils 
```

- [i] On PopOS! the apparmor daemon is initilized by default, but on other distrobutions you may have to do this yourself with the following command: 

```bash
sudo systemctl enable --now apparmor
```

