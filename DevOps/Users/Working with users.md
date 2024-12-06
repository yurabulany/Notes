## Create user
sudo useradd -m -d /home/username -g users -s /bin/bash username

## Add password
sudo passwd username

## Add user to sudo group
sudo usermod -aG sudo username

