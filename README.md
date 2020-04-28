# Prijavni sistem

Prijavni sistem narejen v jquery, php, mysql, bootstrap

## Implementacija v svoj projekt

Če hočete uporabiti prijavni sistem, prenesite datoteke, uvozite podatkovno bazo in spremenite ```db_connect.php``` in , da se ujema s strežnikom in ```js/prijava.js```, po uspešni prijavi.

**Kreiranje podatkovne baze**
```bash
CREATE TABLE uporabniki(
    id int not null primary key AUTO_INCREMENT,
    username nvarchar(20) not null unique,
    password nvarchar(256) not null
)
```

____
**Spremenite spremenljivke, da bodo ustrezale vašemu strežniku.**  
```db_connect.php```  

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
**Spremenite ```if(data==1){}```, da bo ustrezal vaši spletni strani.**  
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

## Kontribucija
Pull requesti so dobrodošli. Za večje spremembe najprej odprite težavo in napišite, kaj želite spremeniti.

## Slike
![prijavna_stran](https://i.imgur.com/0LrMVhf.png)
![prijavna_stran](https://i.imgur.com/vLFZ660.png)
![prijavna_stran](https://i.imgur.com/YTXbcX6.png)
![prijavna_stran](https://i.imgur.com/huHBxaw.png)
![prijavna_stran](https://i.imgur.com/jTIdIcC.png)
