SimpleSpidphp
=============
This is a Fork of SimpleSAMLphp

* [SimpleSAMLphp homepage](https://simplesamlphp.org)
* [SimpleSAMLphp Downloads](https://simplesamlphp.org/download)

Usage
-----

* Install with [Composer](https://getcomposer.org/doc/00-intro.md), run the following command in your project:

```bash
git clone https://github.com/dev4pa/simplespidphp.git
cd simplespidphp
composer install
```

* Creazione cartelle di lavoro per logs e certificati
```bash
mkdir log
chmod 777 -R log
mkdir cert
```

* Creazione di un proprio certificato applicativo per la generazione dei metadati da inviare ad AGID
```bash
openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out cert/saml.crt -keyout cert/saml.pem
```
I files generati da questo comando devono essere configurati nel file config/authsources.php

```
    'nomeservizio-sp' => array(
        'saml:SP',
        'privatekey' => 'saml.pem',
        'certificate' => 'saml.crt',
        // The entity ID of this SP.
        // Can be NULL/unset, in which case an entity ID is generated based on the metadata URL.
        'entityID' => null,
```


* Copia dei file di template per il file di configurazione di simplesamlphp e il file contenente i servizi da esporre con SPID
```bash
cp ../config-template/config.php.spid config/config.php
cp ../config-template/authsources.php.spid config/authsources.php
```
Una volta copiati editarli in modo da personalizzare il proprio server e i propri servizi

