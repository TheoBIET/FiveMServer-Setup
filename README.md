# HOW TO SETTING-UP A FIVEM SERVER ON DEBIAN 10 / UBUNTU 20.04

## GIVE YOU ROOT PERMISSION ON YOUR VPS

1 - `cd /etc/ssh/`
2 - `nano sshd_config`
3 - Change `#PermitRootLogin prohibit-password` to `PermitRootLogin yes`
4 - `service sshd restart`
5 - `sudo -s`

## INSTALLING PACKAGE FOR DATABASE

1 - `apt update && apt upgrade`
2 - `apt install -y apache2 php7.3 php7.3-common php7.3-cli php7.3-mysql php7.3-mbstring php7.3-curl apache2-utils mariadb-server`
3 - `mysql_secure_installation` (All with Y)
4 - `cd /var/www/html && wget https://files.phpmyadmin.net/phpMyAdmin/5.0.2/phpMyAdmin-5.0.2-all-languages.tar.gz`
5 - `tar -xzvf phpMyAdmin-5.0.2-all-languages.tar.gz && rm phpMyAdmin-5.0.2-all-languages.tar.gz && mv phpMyAdmin-5.0.2-all-languages phpmyadmin`
6 - `cd phpmyadmin && mv config.sample.inc.php config.inc.php && nano config.inc.php`
7 - Replace `cookie` with `http`
8 - `cd /etc/php/7.3/apache2/`
9 - `nano php.ini`
10 - CTRL + W to find `post_max_size =` and replace the post_max_size with what you want
11 - CTRL + W to find `upload_max_filesize =` and replace the post_max_size with what you want
12 - `service apache2 restart`

## SETTING-UP DATABASE

1 - `mysql -i -u root`
2 - `use mysql;`
3 - `SELECT plugin FROM user WHERE user='root';`
4 - `UPDATE user SET plugin='' WHERE User='root';`
5 - `FLUSH PRIVILEGES;`
6 - `quit`

You can now connect with YOURPUBLICIP/phpmyadmin

## DOWNLOAD LINUX ARTIFACT FOR FIVEM

1 - `cd /home/debian`
2 - `mkdir SERVERNAME`
3 - `cd SERVERNAME`
4 - Download the latest recommended artifact with `wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/3524-2e2b5cc35d3552c59426f9e2d898b443352307be/fx.tar.xz`
You can find the link at `https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/`
5 - `apt-get install xz-utils`
6 - `tar xf fx.tar.xz && rm fx.tar.xz`
8 - Add your resources and your server.cfg
9 - Start the server with `bash run.sh`
10 - Setting up your txAdmin on `YOURPUBLICIP:40120`
12 - Open FiveM and connect to your server with F8 `connect YOURPUBLICIP:PORT`
11 - Enjoy :)
