# 아파치서버에 ssl을 적용시키고 https를 사용해보자.

```buildoutcfg
letsencrypt부터 설치
sudo apt-get install letsencrypt

ssl 만들기
sudo letsencrypt certonly --webroot --webroot-path=/web/root/ -d domain

apache에 ssl 적용
vi /etc/apache2/sites-available/default-ssl.conf

<IfModule mod_ssl.c>
        <VirtualHost _default_:443>
                ServerAdmin webmaster@localhost

                DocumentRoot /data/www/

                SSLCertificateFile /etc/letsencrypt/live/{domain}/cert.pem
                SSLCertificateKeyFile /etc/letsencrypt/live/{domain}/privkey.pem
                SSLCertificateChainFile /etc/letsencrypt/live/{domain}/chain.pem

sudo a2enmod ssl
sudo a2ensite default-ssl.conf
sudo vi /etc/apache2/apache2.conf

<Directory /web/root/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>

sudo service apache2 restart

```