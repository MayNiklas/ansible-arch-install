# ansible-arch-install
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=lines)](https://github.com/XAMPPRocky/tokei)
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=code)](https://github.com/XAMPPRocky/tokei)
[![Lines Of Code](https://tokei.rs/b1/github/MayNiklas/ansible-arch-install?category=files)](https://github.com/XAMPPRocky/tokei)

### Intro
This ansible-playbook is being used for installing Arch Linux on a new computer. Please make sure, that you understand the underlaying roles and what they do before following my quickstart guide.

### Post install
My arch install is splitted into "pre and postinstall" ansible-playbooks. 
There is a second playbook I'm using after the first reboot:
[ansible-arch](https://github.com/MayNiklas/ansible-arch.git)

### Roles used
- [ansible-arch-setup](https://github.com/MayNiklas/ansible-arch-setup.git)

### Role Variables:
To be set in group_vars OR host_vars

| Variable       | Description                                  | Default |
|----------------|----------------------------------------------|---------|
|`ansible_user`| user used for login into archiso | `root` |
|`user_name`| name of the user being created | `nik` |
|`ansible_host`| ip adress of your computer | `<empty>` |
|`user_password`| hashed pw of the user being created | `<empty>` |
|`hostname`| hostname that should be set | `arch-workstation`|
|`install_drive`| path of the drive being used | `/dev/sda` |
|`bios_partition_suffix`| only relevant when changing the whole task by yourself | `1` |
|`boot_partition_suffix`| efi partion has the partion number 1 | `1` |
|`root_partition_suffix`| root partion has the partion number 2 | `2` |
|`bios`| set to true when you want a bios install -> conflicts with efi | `false` |
|`efi`| set to true when you want a efi install -> conflicts with bios | `false` |
|`intel`| set to true when you want to install intel-ucode & mesa | `false` |
|`amd`| set to true when you want to install amd-ucode | `false` |
|`nvidia`| set to true when you want to install nvidia & nvidia-settings | `false` |
|`bluetooth`| set to true when you want to configure bluetooth | `false` |
|`sshd`| set to true when you want a running sshd server | `false` |
|`xorg`| set to true when you want to install xorg packages | `false` |
|`plasma`| set to true when you want to install plasma & boot into it | `false` |

### Quick start
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
