# Painel V11 Debian 9
 
 
 
 
Source PHP5

nano /etc/apt/source.list

deb http://ftp.debian.org/debian/ jessie main contrib non-free<br>
deb-src http://ftp.debian.org/debian/ jessie main contrib non-free<br>
deb http://security.debian.org/ jessie/updates main contrib non-free<br>
deb-src http://security.debian.org/ jessie/updates main contrib non-free<br>

Comando Depencias

apt update && apt install apache2 mysql-server libssh2-1-dev libssh2-php php5 libapache2-mod-php5 php5-mcrypt php5-curl curl unzip cron mcrypt php5-mysqlnd-ms -y && apt purge php7* && apt autoremove && service apache2 restart

Comando download panel

cd /var/www/html/ && wget https://bigbolgames.com/paineldb9/painelv11debian9penguin.zip && unzip painelv11debian9penguin.zip && rm -R index.html && rm -R painelv11debian9penguin.zip && cd

Comando crontab -e

15 * * * * root /usr/bin/php /var/www/html/pages/system/cron.php<br>
15 * * * * root /usr/bin/php /var/www/html/pages/system/cron.ssh.php<br>
15 * * * * root /usr/bin/php /var/www/html/pages/system/cron.sms.php<br>
15 * * * * root /usr/bin/php /var/www/html/pages/system/cron.online.ssh.php<br>
10 * * * * root /usr/bin/php /var/www/html/pages/system/cron.servidor.php<br>

Comando Chmod 

chmod 777 /var/www/html/admin/pages/servidor/ovpn<br>
chmod 777 /var/www/html/admin/pages/download<br>
chmod 777 /var/www/html/admin/pages/faturas/comprovantes<br>


Editar senha mysql painel

nano /var/www/html/pages/system/pass.php

Comando mysql

mysql -uroot

GRANT ALL ON *.* TO 'root'@'%' IDENTIFIED BY '[sua senha]' WITH GRANT OPTION; 

CREATE USER 'painel'@'%' IDENTIFIED BY 'sua senha';

GRANT ALL PRIVILEGES ON *.* TO 'painel'@'%' WITH GRANT OPTION;

Comando Instalar PHP Myadmin

Nescessario gerar o config-inc.php infelizmente o que estava no backup foi perdido 

cd /var/www/html && wget https://bigbolgames.com/paineldb9/phpMyAdmin-4.9.0.1-english.zip && unzip phpMyAdmin-4.9.0.1-english.zip && mv phpMyAdmin-4.9.0.1-english phpmyadmin && rm -R phpMyAdmin-4.9.0.1-english.zip && cd phpmyadmin

Download SQL Base e instalação

mysql -uroot

Dentro do MYSQL

create database sshplus;

quit

Dentro do Terminal

wget https://bigbolgames.com/paineldb9/penguinehis.sql

mysql -uroot sshplus < penguinehis.sql


Caso de falha na instalção do cliente, use este comando na vps que quer por no painel caso de o Erro SSH ja existe mesmo a vps estando limpa


wget https://bigbolgames.com/paineldb9/scripts.zip && unzip scripts.zip && cd scripts && cp * /root && cd /root && rm -R scripts && chmod 777 * && rm -R scripts.zip


