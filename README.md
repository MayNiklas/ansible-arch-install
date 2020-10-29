# ansible-arch-install
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=lines)](https://github.com/XAMPPRocky/tokei)
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=code)](https://github.com/XAMPPRocky/tokei)
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=files)](https://github.com/XAMPPRocky/tokei)

0. Make sure ansible is on the controller device:
```bash
# arch
sudo pacman -S ansible

# debian
sudo apt-get install ansible

# MacOS
brew install ansible
```
1. To install all the roles needed at the same time with one command, run the following:
```bash
ansible-galaxy install -r requirements.yml
```
2. Insert variables to your own liking:
```bash
vim host_vars/localhost.yml
vim group_vars/localhost.yml
```
The user_password has to be created by using
```bash
mkpasswd --method=sha-512
```
In case you don't want to install whois/mkpasswd on your system:
```bash
docker run --rm -it debian bash
apt update
apt install whois
mkpasswd --method=sha-512
exit
``` 
3. Boot the archiso
4. Set the root password
```bash
passwd
```
5. Set ChallengeResponseAuthentication yes
```bash
vim /etc/ssh/sshd_config
```
6. Restart SSH
```bash
systemctl restart sshd
```
7. Transfer your controllers public key:
```bash
ssh-copy-id root@<ip-adress>
```
8. execute the playbook on your controller device
```bash
ansible-playbook site.yml
```
