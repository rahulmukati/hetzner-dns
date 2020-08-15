<p align="center">
  <a href="https://dns.hetzner.com/" target="_blank"><img src="https://raw.githubusercontent.com/rahulmukati/hetzner-dns/master/hetzner.png" height="175"></a>
</p>

## Hetzner DNS
> All new and simple Hetzner DNS library for PHP.

## Features

* **Lightweight** - Less than 5 KB, portable with only one file

* **Easy** - Extremely easy to learn and use, friendly construction

* **Powerful** - Supports almost all Hetzner DNS features

* **Friendly** - Works well with every PHP frameworks, like Laravel, Codeigniter, Yii, Slim, and framework which supports singleton extension or composer

* **Free** - Under MIT license, you can use it anywhere whatever you want

## Requirement

PHP 5.6+, recommend PHP 7.0+

## Get Started

### Install via composer

Add to composer.json configuration file.
```
$ composer require rahulmukati/hetzner-dns
```

And update the composer
```
$ composer update
```

```php
// If you installed via composer, just use this code to require autoloader on the top of your projects.
require 'vendor/autoload.php';

// Using HetznerDNS namespace
use HetznerDNS\HetznerDNS;

// Initialize
$hdns = new HetznerDNS([
  'api_token' => 'YOURAPITOKENHERE'
]);
```

**Create DNS Zone**
```php
$hdns->createZone([
  'name' => 'example.com', //Required: String
  'ttl' => '3600' //Optional: Integer
]);
```

**Import DNS Zone file**
```php
$body = '$ORIGIN example.com.
$TTL 3600
; SOA Records
@		IN	SOA	ns1.yourdomain.com. dns.yourdomain.com. 2020081403 86400 10800 3600000 3600
; NS Records
@		IN	NS	ns1.yourdomain.com.
@		IN	NS	ns2.yourdomain.com.
; A Records
@		IN	A	192.168.1.1
; CNAME Records
www		IN	CNAME	example.com.';

$hdns->importZoneFile('ZoneIDHere', $body);
```

**Export DNS Zone file**
```php
$hdns->exportZoneFile('ZoneIDHere');
```

**Get all DNS Zones**
```php
$hdns->getZones([
  'name' => '', //Optional: String
  'page' => '', //Optional: Number >= 1
  'per_page' => '', //Optional: Number <= 100
  'search_name' => '', //Optional: String
]);
```

**Get single DNS Zone**
```php
$hdns->getZone('ZoneIDHere');
```

**Update DNS Zone**
```php
$hdns->updateZone('ZoneIDHere', [
  'name' => 'example.com', //Required: String
  'ttl' => '3600' //Optional: Integer
]);
```

**Delete DNS Zone**
```php
$hdns->deleteZone('ZoneIDHere');
```

**Create DNS Record**
```php
$hdns->createRecord([
  'zone_id' => 'ZoneIDHere', //Required: String
  'name' => '@', //Required: String
  'type' => 'CNAME', //Required: String ("A" "AAAA" "NS" "MX" "CNAME" "RP" "TXT" "SOA" "HINFO" "SRV" "DANE" "TLSA" "DS" "CAA")
  'value' => 'example.com', //Required
  'ttl' => '3600' //Optional: Integer
]);
```

**Get all DNS Records**
```php
$hdns->getRecords([
  'zone_id' => 'ZoneIDHere', //Optional: String
  'page' => '1', //Optional: Number
  'per_page' => '10', //Optional: Number
]);
```

**Get single DNS Record**
```php
$hdns->getRecord('RecordIDHere');
```

**Update DNS Record**
```php
$hdns->updateRecord('RecordIDHere', [
  'zone_id' => 'ZoneIDHere', //Required: String (ID of zone this record is associated with)
  'name' => '@', //Required: String
  'type' => 'CNAME', //Required: String ("A" "AAAA" "NS" "MX" "CNAME" "RP" "TXT" "SOA" "HINFO" "SRV" "DANE" "TLSA" "DS" "CAA")
  'value' => 'example.com', //Required
  'ttl' => '3600' //Optional: Integer
]);
```

**Delete DNS Record**
```php
$hdns->deleteRecord('RecordIDHere');
```

