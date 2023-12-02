# Server Configuration

Config linux VPS to run Laravel projects

* `webserver= Nginx`
* `operating system= ubuntu `



### Log in to your server as root:

```bash
ssh root@serveripaddress
```

or with ssh setup

```bash
ssh -i /path to ssh keys.pem root@serveripaddress
```

and run some basic commands:

```bash
sudo apt-get update
```
```bash
sudo apt-get install -y unattended-upgrades
```

### Install Fail2Ban
Fail2Ban is a program for Linux based servers that block hackers by scoring server logs and banning IP addresses with malicious patterns

```bash
sudo apt-get install -y fail2ban
```

### Install Webserver(Nginx)

```bash
sudo apt-get install -y software-properties-common
```
```bash
sudo add-apt-repository ppa:nginx/stable
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install -y nginx
```
```bash
sudo service nginx restart
```
Now visit your servers public IP address in a browser (e.g. http://127.0.0.1)
<p align="center">
<img src="https://miro.medium.com/v2/resize:fit:616/1*jYKmpagQNEkQngqYcyG6bQ.png">
</p>

### Install PHP 7
PHP 7 is required for Laravel 5.7+. Before installing PHP 7 first check if there is no PHP 5 installed. Remove PHP 5 using the following commands:

```bash
sudo apt-get purge php5-fpm
```
```bash
sudo apt-get - purge autoremove
```

Once you are certain the PHP 5 is removed then proceed to install relevant repositories for PHP 7.
```bash
sudo apt-get install -y software-properties-common
```
```bash
sudo apt-get install -y python-software-properties
```
```bash
sudo add-apt-repository ppa:ondrej/php
```
```bash
sudo apt-get update
```

Install and restart PHP 7 using the following commands.
```bash
sudo apt-get install -y php7.4 php7.4-fpm php-mysql php7.4-mysql php-mbstring libapache2-mod-php7.4 php-doctrine-dbal php7.4-pgsql php-xml redis-server
```
```bash
sudo systemctl restart php7.4-fpm
```

### Install PHP 8
```bash
sudo apt-get install -y php8.2 php8.2-fpm php-mysql php8.2-mysql php-mbstring libapache2-mod-php8.2 php-doctrine-dbal php8.2-pgsql php-xml redis-server
```
```bash
sudo systemctl restart php8.2-fpm
```

### Install Composer
update the package manager cache by running
```bash
sudo apt update
```
run the following command to install the required packages
```bash
sudo apt install php-cli unzip
```
Make sure you’re in your home directory, then retrieve the installer using curl:
```bash
cd ~
```
```bash
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
```
```bash
sudo apt install php-cli unzip
```
Next, we’ll verify that the downloaded installer matches the SHA-384 hash for the latest installer found on the **[Composer Public Keys / Signatures](https://composer.github.io/pubkeys.html)** page.
To facilitate the verification step, you can use the following command to programmatically obtain the latest hash from the Composer page and store it in a shell variable:
```bash
HASH=`curl -sS https://composer.github.io/installer.sig`
```
If you want to verify the obtained value, you can run:
```bash
echo $HASH
```
Now execute the following PHP code, as provided in the Composer **[download page](https://getcomposer.org/download/)**, to verify that the installation script is safe to run
```bash
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```
To install composer globally, use the following command which will download and install Composer as a system-wide command named composer, under /usr/local/bin:
```bash
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```
To test your installation, run:
```bash
composer
```




