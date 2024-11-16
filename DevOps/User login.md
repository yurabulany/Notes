## Password entry
For password entry need to append the /etc/ssh/sshd_config file:
`Match User username
`PasswordAuthentification yes`

## SSH login
For ssh login the steps are the following
1. Generate the SSH key on the host machine 
2. Login to VM from the user
3. Create ~/.ssh on VM 
4. Create ~/.ssh/authorized_keys file
5. Copy the ssh key to ~/.ssh/authorized_keys file 
6. Make the ~/.ssh folder is executable by the user `chmod 700 ~/.ssh`
7. Make the ~/.ssh/authorized_keys file read-write by the user `chmod 600 ~/.ssh/authorized_keys`




