Create folder `ssl`
Open folder `ssl` in console

Run command: `openssl req -newkey rsa:2048 -nodes -keyout localhost.key -x509 -days 365 -out localhost.crt`

OR command: `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout localhost.key -out localhost.crt -subj "/C=CA/ST=Alberta/L=Calgary/O=MyCompany/CN=localhost" `

Standard path to docker php ``/usr/local/bin/php``

Change path in mac: `sudo vim /etc/hosts`