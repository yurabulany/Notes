## Script

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

## Systemd service

[Unit] 
Description=Write uptime to file every 15 seconds 
After=network.target 

[Service] ExecStart=/home/vagrant/uptime.sh 
Restart=always 
RestartSec=5 
User=root 

[Install] WantedBy=multi-user.target