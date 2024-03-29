# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - Николай Копосов



### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

### Решение 1
Разрешены [службы](/files/slushby.txt)

- 21/tcp    open  ftp
- 22/tcp    open  ssh
- 23/tcp    open  telnet
- 25/tcp    open  smtp
- 53/tcp    open  domain
- 80/tcp    open  http
- 111/tcp   open  rpcbind
- 139/tcp   open  netbios-ssn
- 445/tcp   open  microsoft-ds
- 512/tcp   open  exec
- 513/tcp   open  login
- 514/tcp   open  shell
- 1099/tcp  open  unknown
- 1524/tcp  open  ingreslock
- 2049/tcp  open  nfs
- 2121/tcp  open  ccproxy-ftp
- 3306/tcp  open  mysql
- 3632/tcp  open  distccd
- 5432/tcp  open  postgres
- 5900/tcp  open  vnc
- 6000/tcp  open  X11
- 6667/tcp  open  irc
- 6697/tcp  open  unknown
- 8009/tcp  open  ajp13
- 8180/tcp  open  unknown
- 8787/tcp  open  unknown
- 36360/tcp open  unknown
- 46088/tcp open  unknown
- 48314/tcp open  unknown
- 53212/tcp open  unknown

В установленных версиях [ПО](/files/nmapsV.txt) нашел уязвимости:

- [vsftpd 2.3.4 - Backdoor Command Execution](https://www.exploit-db.com/exploits/49757)
- [UnrealIRCd 3.2.8.1 - Backdoor Command Execution (Metasploit)](https://www.exploit-db.com/exploits/16922)
- [не нашел на exploit db, но много информации просто по поиску версии Apache httpd 2.2.8 ((Ubuntu) DAV/2)](https://spy-soft.net/hacking-http-port-80/)
- [Samba (порты 139 и 445): Уязвимости в Samba smbd 3.X могут привести к несанкционированному доступу к файлам и ресурсам на сервере.](https://www.exploit-db.com/exploits/42060)
- [rpcbind](https://www.exploit-db.com/exploits/26887) 


----------------------------


### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

### Решение 2:

 Различия между режимами сканирования:

- [SYN](/files/nmapsS.txt) сканирование: Отправляет SYN пакеты для определения открытых портов. Если целевая система отвечает SYN+ACK, то порт открыт.
- [FIN](/files/nmapsF.txt) сканирование: Отправляет FIN пакеты для определения открытых портов. Если целевая система не отправляет RST пакет в ответ, то порт открыт.
- [Xmas](/files/nmapsX.txt) сканирование: Отправляет пакеты с установленными FIN, URG и PSH флагами для определения открытых портов. Если целевая система не отправляет RST пакет в ответ, то порт открыт.
- [UDP](/files/nmapsU.txt) сканирование: Отправляет UDP пакеты для определения открытых портов. Если целевая система отправляет ICMP пакет с сообщением "Port Unreachable", то порт закрыт.