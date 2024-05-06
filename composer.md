# Composer

Prior to this PHP needs to be installed

## Install latest Composer

```
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ php -r "unlink('composer-setup.php');"
$ php composer-setup.php
```

To be globally accessible move PHAR(php archive) in bin folder

```
$ mv composer.phar /usr/local/bin/composer
```
