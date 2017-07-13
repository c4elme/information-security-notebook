1. Create new workspace and clone the laravel app
2. run the following command `$ sudo nano /etc/apache2/sites-available/001-cloud9.conf` and change the server root or something to redirect it to the public folder.
3. Make sure that the workspace has the latest version of php, if not, follow this instruction \(source: [https://community.c9.io/t/phpbrew-on-php-workspaces/621/3\](https://community.c9.io/t/phpbrew-on-php-workspaces/621/3\)\)

   1. You can use`phpbrew`on Cloud9. I found that the standard installation process works fine, just run the commands below.  
         We first install the`libmcrypt-dev`package to avoid running into dependency issues during build:

      ```
         $ sudo apt-get update
         $ sudo apt-get install libmcrypt-dev
      ```

      Next, we download`phpbrew`and move it to`/usr/local/bin`:

      ```
         $ curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew
         $ chmod +x phpbrew
         $ sudo mv phpbrew /usr/local/bin/
         $ phpbrew init

         # add this to your ~/.bashrc
         $ [[ -e ~/.phpbrew/bashrc ]] 
         &
         &
          source ~/.phpbrew/bashrc

         $ phpbrew lookup-prefix ubuntu
      ```

      Once set up, we install and load PHP 5.6:

   ```
   $ phpbrew install 5.6 +default
   $ phpbrew switch php-5.6.31
   $ phpbrew use php-5.6.31
   $ php -v
   PHP 5.6.31 (cli) (built: Dec 29 2015 21:31:19)
   Copyright (c) 1997-2015 The PHP Group
   Zend Engine v2.6.0, Copyright (c) 1998-2015 Zend Technologies    
   ```

4. Now run the composer install command to install the dependencies of the laravel application

5. If problems occured, make sure that the php5.6 is enabled

   1. ```
      sudo add-apt-repository ppa:ondrej/php
      ```

      ```
      sudo apt-get update
      sudo apt-get purge php5-common # remove and purge old PHP 5.x packages
      sudo apt-get install libapache2-mod-php5.6
      ```







