# ansible-arch-install
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
3. Boot the archiso
4. Set the root password using  passwd.
5. Set ChallengeResponseAuthentication yes
```bash
vim /etc/ssh/sshd_config
```
6. Restart SSH
```bash
systemctl restart sshd
```
7. execute the playbook on your controller device
```bash
ansible-playbook site.yml
```
