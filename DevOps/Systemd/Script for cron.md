## Script

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

## Cron command 
```
sudo crontab -e path/to/script

*/10 * * * * /bin/bash /path/to/script
```