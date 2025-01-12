## User manipulation

1. Create a user `sudo useradd -m -d /home/username -g users -s /bin/bash username`
2. Add password for user `sudo passwd username`
3. Add user to group (sudo group) `sudo usermod -aG sudo username`
4. Change shell for a user `sudo chsh -i (if not the same user) /bin/sh username`

## Login
### Password login
For password entry need to append the /etc/ssh/sshd_config file:
`Match User username
`PasswordAuthentification yes`

### SSH login
For SSH entry need to append the /etc/ssh/sshd_config file:
`Match User username
`PasswordAuthentification yes`

For ssh login the steps are the following
1. Generate the SSH key on the host machine 
2. Login to VM from the user
3. Create ~/.ssh on VM 
4. Create ~/.ssh/authorized_keys file
5. Copy the ssh key to ~/.ssh/authorized_keys file 
6. Make the ~/.ssh folder executable by the user `chmod 700 ~/.ssh`
7. Make the ~/.ssh/authorized_keys file read-write by the user `chmod 600 ~/.ssh/authorized_keys`

### Users on ec2 machine (vm name - users)
Raymond (ssh, password - test)

John (password - test)

steve (password - test)


## Copy a file from local to remote
scp -i /path/to/sshkey /path/to/localfile username@ipaddress:/path/to/directory
