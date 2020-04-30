# Login System

Login System made in  **jQuery, PHP, MySQL, Bootstrap**.

## Implementation

If you want to use this login system, clone the repo, import the database and change the ```db_connect.php``` variables, that fit your credentials in the server. You also need to change the ```js/prijava.js``` so that it redirects to your desired url after a successful login.

**Creating the database**
```bash
CREATE DATABASE db;

use db;

CREATE TABLE uporabniki(
    id int not null primary key AUTO_INCREMENT,
    username nvarchar(20) not null unique,
    password nvarchar(256) not null
)
```

____
**Change the variables**  
```php_handle/db_connect.php```  

```bash
<?php
// spremenljivke za povezavo na bazo
$servername = "localhost"; # ime strežnika
$username = "root"; # uporabniško ime serverja
$password = ""; # geslo serverja
$baza = "opravila"; # podatkovna baza

// objekt za novo povezavo
$conn = new mysqli($servername, $username, $password, $baza);

// v primeru, da se server poveže na bazo
if ($conn->connect_error) {
    die("Povezava ni uspela: " . $conn->connect_error);
}
 ?>
```

____
**Change ```if(data==1){}```, to your desired url.**  
```js/prijava.js```
```bash
// preveri ce so vsi DOM elementi ustvarjeni
$(document).ready(function(){
  // caka na klik gumba (prijavi)
  $("#gumb_p").click(function(data){
    // spremenljivka uporabniskega imena (input text)
    var username = $("#username").val();
    // spremenljivka gesla (input password)
    var password = $("#password").val();
    var error = false;

    if(username.length < 3){
      error = true;
      $("#username").css("border", "1px solid red");
      $("#info").html("Uporabniško ime mora biti dolgo vsaj 3 črke");
    }

    // preveri ce sta polja prazna
    if(username == "" && password == "" && error == false){
      // nastavi span html vrednost z idjem #info
      $("#info").html("Vnesi vsa polja!");
    }else{
      // POST request na php_handle/prijavi.php, prijavi.php vrne parameter data
      $.ajax({
          type: "POST",
          url: "php_handle/prijavi.php",
          data:{username:username, password:password},
          success: function(data){
            if(data == 1){
              // Spremeni na svoj custom url (redirect)
            }else {
              $("#username").css("border", "1px solid red");
              $("#password").css("border", "1px solid red");
              $("#info").html("Uporabniško ime in geslo se ne ujemata!")
            }
          }
      });
    }
  });
});


```

## Contribution
Pull requests are welcome.

## Slike
![prijavna_stran](https://i.imgur.com/0LrMVhf.png)
![prijavna_stran](https://i.imgur.com/vLFZ660.png)
![prijavna_stran](https://i.imgur.com/YTXbcX6.png)
![prijavna_stran](https://i.imgur.com/huHBxaw.png)
![prijavna_stran](https://i.imgur.com/jTIdIcC.png)
