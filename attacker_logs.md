2. Од логовите во фајлот во прилог, дали забележувате малиционзи активности? Ако има, од каде доаѓаат, и какви се (може да има повеќе од еден вид). Дали по вас овој сајт е хакиран или само има неуспешни обиди? Спремете си белешки или список за на интервјуто: како ги баравте ранливостите, што најдовте, што треба да направи администраторот (може и ништо не треба).

# prvo sto mi tekna da napravam, sekoja IP adresa da proveram sto sakala da napravi i od koj operativen sistem ako ima vrska, tie IP adresi sto nemaat znaci na napad ne se navedeni.

### 45.33.49.201
- ovaa IP adresa e totalno somnitelna vednas, pocnuva so prebaruvanje na .robots.txt, .git, .env, /config.php, probuva da dojde do admin login page, kaj sto mu dava 404 errors, /admin mu pravi redirect, se dodeka ne dobie 200 ok request so /admin/login.php, togas ocigledno probuva so bruteforce da go probie passwordot so login requests na sekoi 3 sekundi, po nekoe vreme se logira na dashboard.php, simnuva backup zip file so site podatoci, potoa prikacuva shell.php malicious file so ok requests, i gi menuva podatocite so user-edit.php, najverojatno napadot e uspesen, site podatoci se zemeni i moze da bidat zloupotrebeni. Koristeni se povekje operativni sistemi.
##### Koristeni maliciozni aktivnosti: Brute-force, baranje cuvstvitelni fajlovi, WEB SHELL ATTACK, RCE kontrola preku shell.php

### 198.51.100.73
- isto probuva da XSS napad vo URL-to na blog comment, SQL injection vo search field, posle so bruteforce probuva da go smeni passwordot na admin userot, i se gleda deka tokenot raboti kako sto treba, sto e mnogu bitno vo security zaradi vakvi raboti, ne bi trebalo da e uspesen ovoj obid, osven ako ne e istiot so IP 45.33.49.201 , sto e mnogu mozno zatoa sto mnogu cesto napagjacot gi menuva IP adresite za napadi.
##### Koristeni maliciozni aktivnosti: XSS (Cross-Site Scripting), SQL ili Command Injection, Brute-force, Path Traversal, obid za neovlasten pristap

### 121.18.83.75
- prvo so SQL injection i enkodirani karakteri , kaj sto dava 500 error neuspesen obid, posle probuva so path traversal so ../../etc/passwd, isto i so XSS script tag 400 error bad request, i command injection kaj sto mu dava 404 not found. ima i obid so /api/user1/profile i /api/user2/profile da proba da gi prikaze korisnicite neovlasteno. isto taka moze da e istiot attacker so smeneta ip adresa.
##### Koristeni maliciozni aktivnosti: XSS (Cross-Site Scripting), SQL ili CommandInjection, Path Traversal, obid za neovlasten pristap, obidi za otkrivanje na sistemot so api endpoints

### 216.58.212.110
- ovaa IP adresa koristi Postman, alatka za testiranje na API, probuva da pristapi kon /api/users 403 forbidden error, obidi za kreiranje naracki, prviot neuspesen, vtoriot uspesen, mnogu e mozno da e tester ili attacker sto gi testira API endpoints. isto taka ima i neobicni parametri, sto moze da bide ili greska vo urlto ili obid za API manipulacija. Moze da e prethodnik na napadi kako Brute-force ili API abuse.
##### Koristeni maliciozni aktivnosti: API scan, auth test
