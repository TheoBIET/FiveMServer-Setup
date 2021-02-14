# HOW TO SETTING-UP A FIVEM SERVER ON DEBIAN 10 / UBUNTU 20.04

## GIVE YOU ROOT PERMISSION ON YOUR VPS

- `cd /etc/ssh/`
- `nano sshd_config`
- Change `#PermitRootLogin prohibit-password` to `PermitRootLogin yes`
- `service sshd restart`
- `sudo -s`

## INSTALLING PACKAGE FOR DATABASE

- `apt update && apt upgrade`
- `apt install -y apache2 php7.3 php7.3-common php7.3-cli php7.3-mysql php7.3-mbstring php7.3-curl apache2-utils mariadb-server`
- `mysql_secure_installation` (All with Y)
- `cd /var/www/html && wget https://files.phpmyadmin.net/phpMyAdmin/5.0.2/phpMyAdmin-5.0.2-all-languages.tar.gz`
- `tar -xzvf phpMyAdmin-5.0.2-all-languages.tar.gz && rm phpMyAdmin-5.0.2-all-languages.tar.gz && mv phpMyAdmin-5.0.2-all-languages phpmyadmin`
- `cd phpmyadmin && mv config.sample.inc.php config.inc.php && nano config.inc.php`
- Replace `cookie` with `http`
- `cd /etc/php/7.3/apache2/`
- `nano php.ini`
- CTRL + W to find `post_max_size =` and replace the post_max_size with what you want
- CTRL + W to find `upload_max_filesize =` and replace the post_max_size with what you want
- `service apache2 restart`

## SETTING-UP DATABASE

- `mysql -i -u root`
- `use mysql;`
- `SELECT plugin FROM user WHERE user='root';`
- `UPDATE user SET plugin='' WHERE User='root';`
- `FLUSH PRIVILEGES;`
- `quit`

You can now connect with YOURPUBLICIP/phpmyadmin

## DOWNLOAD LINUX ARTIFACT FOR FIVEM

- `cd /home/debian`
- `mkdir SERVERNAME`
- `cd SERVERNAME`
- Download the latest recommended artifact with `wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/3524-2e2b5cc35d3552c59426f9e2d898b443352307be/fx.tar.xz`
You can find the link at `https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/`
- `apt-get install xz-utils`
- `tar xf fx.tar.xz && rm fx.tar.xz`
- Add your resources and your server.cfg
- Start the server with `bash run.sh`
- Setting up your txAdmin on `YOURPUBLICIP:40120`
- Open FiveM and connect to your server with F8 `connect YOURPUBLICIP:PORT`
- Enjoy :)
