# Домашнее задание к занятию 12.1 "Уязвимости и атаки на информационные системы" Корнилов Андрей



### Задание 1.

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
Приведите ответ в свободной форме.

### Ответ
```
Просканировава командой nmap нашу машину мы увидим доступные сетевые службы.

Starting Nmap 7.80 ( https://nmap.org ) at 2025-02-05 13:09 +04
Nmap scan report for 10.0.3.65
Host is up (0.00011s latency).
Not shown: 977 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown

Какие уязвимости были вами обнаружены?

OpenSSH 4.7p1
Уязвимость: User Enumeration
CVE-идентификатор: CVE-2008-1483
Ссылка на эксплойт: https://www.exploit-db.com/exploits/6100

Postfix (smtp)
Уязвимость: SMTP Command Injection
CVE-идентификатор: CVE-2008-2939
Ссылка на эксплойт: https://www.exploit-db.com/exploits/6406

Apache HTTP Server 2.2.8
Уязвимость: Remote Code Execution
CVE-идентификатор: CVE-2009-3555
Ссылка на эксплойт: https://www.exploit-db.com/exploits/9444

Samba 3.X - 4.X
Уязвимость: Remote Code Execution
CVE-идентификатор: CVE-2017-7494
Ссылка на эксплойт: https://www.exploit-db.com/exploits/41998

MySQL 5.0.51a
Уязвимость: Unauthorized Access to MySQL Database
CVE-идентификатор: CVE-2010-4018
Ссылка на эксплойт: https://www.exploit-db.com/exploits/11450
```

### Задание 2.
Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
Как отвечает сервер?
Приведите ответ в свободной форме.

### Ответ
```
SYN-сканирование:
Использует полуоткрытые соединения (отправляет SYN, получает SYN-ACK для открытых портов).
Быстрое и менее заметное, так как соединение не завершается.

FIN-сканирование:
Отправляет FIN-пакеты без установления соединения.
Эффективно для обхода некоторых firewall, которые не отслеживают состояния соединений.

Xmas-сканирование:
Аналогично FIN-сканированию, но использует пакеты с несколькими флагами (FIN, PSH, URG).
Может быть полезно для выявления нестандартных реакций сервера.

UDP-сканирование:
Использует UDP-пакеты вместо TCP.
Медленнее, так как UDP не гарантирует доставку, и сервер может не отвечать.

Как отвечает сервер?

SYN-сканирование:
Открытый порт: SYN-ACK.
Закрытый порт: RST.

FIN-сканирование:
Открытый порт: Нет ответа.
Закрытый порт: RST.

Xmas-сканирование:
Открытый порт: Нет ответа.
Закрытый порт: RST.

UDP-сканирование:
Открытый порт: UDP-ответ (если служба активна).
Закрытый порт: ICMP "Port Unreachable".
