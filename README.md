# Magento Basic

    - Magento Basic Version 2.4.5

## Process

    - Download and Install Git Bash
    - Download and Install xampp php v.8
    - Download and Install composer
    - Download Elastic Search and extract to C:\xampp\htdocs

## XAMPP Enable PHP extensions and Configure (php.ini)

    - Enable PHP (php.ini) {extension=gd}
    - Enable PHP (php.ini) {extension=intl}
    - Enable PHP (php.ini) {extension=soap}
    - Enable PHP (php.ini) {extension=xsl}
    - Enable PHP (php.ini) {extension=sockets}
    - Enable PHP (php.ini) {extension=sodium}
    - Remove the semicolone " ; " of the php.ini extensions
    - Update
        - max_execution_time=120 to 18000
        - max_input_time=60 to 1800
        - memory_limit=512M to 4G

## Download Magento Command

    - composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.5

## Authentication required repo.magento.com:

    - Create account Magento Marketplace in click the link below

[Magento Marketplace](https://marketplace.magento.com/)

    - Then goto My Profile click the link below

[My Profile](https://marketplace.magento.com/customer/account/)

    - Click the Access Keys - Then Click the (Create A New Access Key) name it what you want.

    - Username: public key
    - Password: private key

## Run

    - Run Elastic search,
    - Xampp apache and mysql

## Goto

    - C:\xampp\htdocs\project-community-edition\vendor\magento\framework\Image\Adapter\Gd2.php

```
    private function validateURLScheme(string $filename) : bool {
        $allowed_schemes = ['ftp', 'ftps', 'http', 'https'];
        $url = parse_url($filename);
        if ($url && isset($url['scheme']) && !in_array($url['scheme'], $allowed_schemes) && !file_exists($filename)) {
            return false;
        }
        return true;
    }

```

    - C:\xampp\htdocs\project-community-edition\vendor\magento\framework\View\Element\Template\File\Validator.php

        $realPath = $this->fileDriver->getRealPath($path);

        Replace with this code:

        $realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));

## Add entry in host files:

    - C:\xampp\apache\conf\extra\httpd-vhosts.conf

```
        <VirtualHost *:80>
            DocumentRoot "C:/xampp/htdocs/project-community-edition/pub"
            ServerName dev.magento.com
        </VirtualHost>
        <VirtualHost *:80>
            DocumentRoot "C:/xampp/htdocs"
            ServerName localhost
        </VirtualHost>
```

    - C:\Windows\System32\drivers\etc\hosts

        127.0.0.1   dev.magento.com

## Magento SETUP

```
php bin/magento setup:install --base-url="http://dev.magento.com/" --db-host="localhost" --db-name="magento245" --db-user="root" --db-password="" --admin-firstname="admin1" --admin-lastname="admin1" --admin-email="user@example.com" --admin-user="admin1" --admin-password="admin1@12345" --language="en_US" --currency="USD" --timezone="America/Chicago" --use-rewrites="1" --backend-frontname="admin1" --search-engine=elasticsearch7 --elasticsearch-host="localhost" --elasticsearch-port=9200
```

## Replace Line In app/etc/di.xml in magento file path

    Magento\Framework\App\View\Asset\MaterializationStrategy\Symlink

    TO:

    Magento\Framework\App\View\Asset\MaterializationStrategy\Copy

## Disable extension:

    php bin/magento module:disable Magento_TwoFactorAuth
    php bin/magento setup:di:compile
    php bin/magento cache:flush

## Run These Magento Commands:

    php bin/magento sampledata:deploy

    php bin/magento indexer:reindex
    php bin/magento setup:upgrade
    php bin/magento setup:static-content:deploy -f
    php bin/magento cache:flush

## Clean Page 
    php bin/magento cache:clean full_page
