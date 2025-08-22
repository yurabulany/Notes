## Jobs

`jobs` - to view the list of running jobs

CTRL + Z to suspend the job

`fg %1` - to resume the process in foreground

`bg %1` - to resume the process in background

`ping 8.8.8.8 &` - starts ping in the background

`kill %1`- stops the process completely

## Cron

### Script

```
#!/bin/bash

# Название systemd-юнита
unit_name="write_uptime.service"

# Лог-файл для записи статуса
log_file="/var/log/unit_status.log"

# Проверяем статус юнита
status=$(systemctl is-active "$unit_name")

# Записываем статус в лог
echo "$(date): Unit '$unit_name' is $status" >>"$log_file"

# Если юнит не активен, попытаться перезапустить его
if [[ "$status" != "active" ]]; then
  echo "$(date): Attempting to restart '$unit_name'" >>"$log_file"
  systemctl restart "$unit_name"
fi
```

### Cron command

```
sudo crontab -e path/to/script

*/10 * * * * /bin/bash /path/to/script
```

## Systemd

### Uptime script

```
#!/bin/bash

while true; do
    # Получаем значение Load Average за 1 минуту
    load_avg=$(uptime | awk -F 'load average: ' '{print $2}' | awk -F ',' '{print $1}')
    
    # Получаем размер файла
    file_size=$(stat --format=%s /home/vagrant/overload.txt)

    # Сравниваем значение с 1
    if (( $(echo "$load_avg > 1" | bc -l) )); then
        echo "$(date): $load_avg" >> /home/vagrant/overload.txt
    elif (( $(echo "$load_avg <= 1" | bc -l) )); then
        uptime >> /home/vagrant/uptime.txt
    fi

    # Проверяем размер файла overload и очищаем его, если размер больше 50KB
    if (( file_size > 50000 )); then
        echo "$(date): File size exceeded 50KB, clearing overload.txt" >> cleanup.txt
        > /home/vagrant/overload.txt  # Очищаем файл
    fi

    # Задержка 15 секунд перед следующим циклом
    sleep 15
done
```

### Systemd service

Enable and start the script `sudo systemctl enable service && sudo systemctl start service`

```
[Unit] 
Description=Write uptime to file every 15 seconds 
After=network.target 

[Service] ExecStart=/home/vagrant/uptime.sh 
Restart=always 
RestartSec=5 
User=root 

[Install] WantedBy=multi-user.target

