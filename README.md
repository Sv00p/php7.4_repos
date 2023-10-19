# php7.4_repos
to add the key needed for the PHP repository.
install debian 12 php 7.4 phpmyadmin mysql apache2

```apt update && apt upgrade -y && apt install sudo -y && apt install mc -y && apt install htop -y && apt install curl -y && apt install nmap -y && apt install tcpdump -y && apt install cntlm -y && apt install jo -y && apt install pigz -y && apt install rsyslog -y && apt install sl -y && apt install screenfetch -y && apt install chrony -y  && apt install fping -y && apt install smartmontools -y && apt install hwinfo -y && apt install cpu-checker -y && apt install cifs-utils && apt install lnav && apt install snmp && apt install snmp-mibs-downloader -y && apt install strace -y && apt install xfsdump -y && apt install rsync -y ```



apt install ca-certificates apt-transport-https lsb-release gnupg curl nano unzip -y


add-key:
curl -fsSL https://github.com/Sv00p/php7.4_repos.git -o /usr/share/keyrings/php-archive-keyring.gpg


add-repo
echo "deb [signed-by=/usr/share/keyrings/php-archive-keyring.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

apt update && apt install apache2 -y && apt install php7.4 php7.4-cli php7.4-common php7.4-curl php7.4-gd php7.4-intl php7.4-json php7.4-mbstring php7.4-mysql php7.4-opcache php7.4-readline php7.4-xml php7.4-xsl php7.4-zip php7.4-bz2 libapache2-mod-php7.4 -y


apt install mariadb-server mariadb-client -y

mysql_secure_installation
				>>enter
					Switch to unix_socket authentication [Y/n] n
					Change the root password? [Y/n] y     enter password
					Remove anonymous users? [Y/n] y
					Disallow root login remotely? [Y/n] y
						Remove test database and access to it? [Y/n] y
						Reload privilege tables now? [Y/n] y
						
						
cd /usr/share && wget https://github.com/Sv00p/php7.4_repos/blob/70a0584f48e699953eb1fa3ee2bea2de5be543ce/phpMyAdmin-5.2.1-all-languages.zip -O phpmyadmin.zip

unzip phpmyadmin.zip && rm phpmyadmin.zip

Now you have to rename the directory to "phpmyadmin". Use this command (Теперь вам нужно переименовать каталог в «phpmyadmin». Используйте эту команду)
mv phpMyAdmin-*-all-languages phpmyadmin

chmod -R 0755 phpmyadmin


nano /etc/apache2/conf-available/phpmyadmin.conf

 #phpMyAdmin Apache configuration

Alias /phpmyadmin /usr/share/phpmyadmin

<Directory /usr/share/phpmyadmin>
    Options SymLinksIfOwnerMatch
    DirectoryIndex index.php
</Directory>

# Disallow web access to directories that don't need it
<Directory /usr/share/phpmyadmin/templates>
    Require all denied
</Directory>
<Directory /usr/share/phpmyadmin/libraries>
    Require all denied
</Directory>
<Directory /usr/share/phpmyadmin/setup/lib>
    Require all denied
</Directory>


Save your changes to the configuration by pressing CTRL + X, then hit the "Y" key followed by enter.



a2enconf phpmyadmin
a2enmod rewrite
mkdir /usr/share/phpmyadmin/tmp/


Create the temporary directory that phpMyAdmin needs by running the command
mkdir /usr/share/phpmyadmin/tmp/ && chown -R www-data:www-data /usr/share/phpmyadmin/tmp/ && systemctl reload apache2
