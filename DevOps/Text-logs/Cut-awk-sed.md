cut - используется для извлечения части строки из файла или ввода стандартного потока данных.

Вывести размеры разделов диска в отдельный файл. Отсортировать количество столбцов до трех, оставив только Filesystem, Use%, Mounted on.
`df -h | awk '{print $1, $5, $6}' | sort -n -k2 | column -t > file.txt`
or (without sorting)
`df -h | awk '{print $1, $5, $6}' | column -t > file.txt`

Узнать размер всех файлов и папок в директории /etc. Отсортировать вывод так, чтобы показывало только 10 самых больших файлов.
`ls -l -S -h /etc/ | awk '{print $5, $9}' | column -t | head -10`

Вывести пронумерованные строчки из /etc/passwd, в которых есть оболочка /bin/bash, и перенаправить вывод в файл.
` awk '{print NR, $0}' /etc/passwd | grep 'bash' > file.txt`

Заменить все строчки с /bin/fish на /bin/bash(проводить на бэкапе).
`sed -i 's/fish/bash/g' file.txt`

Вывести строки NDS/A и NAD/A из файла используя awk или sed(regexp)
`sed -n '/^N[DA]/p' file.txt`