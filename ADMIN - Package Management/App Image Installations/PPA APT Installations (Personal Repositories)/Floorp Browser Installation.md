
*To install floorp browser, you will need to add the private repository from a PPA nelonging to Floorp Development team... The following commands will install floor
```bash
curl -fsSL https://ppa.ablaze.one/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/Floorp.gpg
```

```bash
sudo curl -sS --compressed -o /etc/apt/sources.list.d/Floorp.list 'https://ppa.ablaze.one/Floorp.list'
```

```bash
sudo apt update && sudo apt full-upgrade
```

```bash
sudo apt install floorp
```


