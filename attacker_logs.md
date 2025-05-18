2. Од логовите во фајлот во прилог, дали забележувате малиционзи активности? Ако има, од каде доаѓаат, и какви се (може да има повеќе од еден вид). Дали по вас овој сајт е хакиран или само има неуспешни обиди? Спремете си белешки или список за на интервјуто: како ги баравте ранливостите, што најдовте, што треба да направи администраторот (може и ништо не треба).

## Pri analiza na sekoja IP adresa, timestamp, operativen sistem, gi zabelezav slednive somnitelni aktivnosti:

## 45.33.49.201
Ovaa IP adresa e somnitelna vednas, pocnuva so prebaruvanje na .robots.txt, .git, .env, /config.php, probuva da dojde do admin login page, kaj sto mu dava 404 errors, /admin mu pravi redirect, se dodeka ne dobie 200 ok request so /admin/login.php, togas ocigledno probuva so bruteforce da go probie passwordot so login requests na sekoi 3 sekundi, po nekoe vreme se logira na dashboard.php, simnuva backup zip file so site podatoci, potoa prikacuva shell.php malicious file so ok requests, i gi menuva podatocite so user-edit.php, najverojatno napadot e uspesen, site podatoci se zemeni i moze da bidat zloupotrebeni. Koristeni se povekje operativni sistemi.
#### Koristeni maliciozni aktivnosti: 
- Skeniranje na cuvstvitelni fajlovi
- Brute-force
- WEB SHELL ATTACK
- RCE kontrola preku shell.php
#### Preporaki: 
- ITNO BLOKIRANJE NA IP ADRESATA
- PROMENA NA SITE LOZINKI
- zastita od Brute-force napadi so rate limit, reCAPTCHA i 2 factor auth
- otstranuvanje vednas na site shell.php i slicni fajlovi so skeniranje na serverot i proverka na timestap
- zastita na site cuvstvitelni datoteki
- azuriranje na aplikacijata
- aktivacija na WAF
- organiziran backup
- proverka na logovite za tragi na napagjacot
- informiranje na korisnicite ako ima krazba na licni podatoci za zastita

## 198.51.100.73
Pocnuva so XSS napad vo URL-to na blog comment, SQL injection vo search field, posle so bruteforce probuva da go smeni passwordot na admin userot, i se gleda deka tokenot raboti kako sto treba, sto e mnogu bitno vo security zaradi vakvi raboti, ne bi trebalo da e uspesen ovoj obid, osven ako ne e istiot so IP 45.33.49.201 , sto e mnogu mozno zatoa sto mnogu cesto napagjacot gi menuva IP adresite za napadi.
#### Koristeni maliciozni aktivnosti: 
- XSS (Cross-Site Scripting)
- SQL ili Command Injection
- Brute-force
- Path Traversal
- obid za neovlasten pristap
#### Preporaki: 
- blokiranje na IP adresata vednas
- proverka na site logovi
- update na aplikacijata za da se popravat SQL i XSS injections
- zastita od Brute-force napadi

## 121.18.83.75
SQL injection i enkodirani karakteri , kaj sto dava 500 error neuspesen obid, isto taka probuva so path traversal so ../../etc/passwd, isto i so XSS script tag 400 error bad request, i command injection kaj sto mu dava 404 not found. ima i obid so /api/user1/profile i /api/user2/profile da proba da gi prikaze korisnicite neovlasteno. isto taka moze da e istiot attacker so smeneta ip adresa, zasto dobiva 200 error so api/info i potoa 45.33.49.201 se logira na admin.
#### Koristeni maliciozni aktivnosti: 
- XSS (Cross-Site Scripting)
- SQL ili CommandInjection
- Path Traversal
- obid za neovlasten pristap
- obidi za otkrivanje na sistemot so api endpoints
#### Preporaki: 
- blokiranje na IP adresata vednas
- proverka na site logovi
- update na aplikacijata za da se popravat SQL i XSS injections
- ogranicuvanje na API povici

## 216.58.212.110
Koristi Postman, alatka za testiranje na API, probuva da pristapi kon /api/users 403 forbidden error, obidi za kreiranje naracki, prviot neuspesen, vtoriot uspesen, mnogu e mozno da e tester ili attacker sto gi testira API endpoints. isto taka ima i neobicni parametri, sto moze da bide ili greska vo urlto ili obid za API manipulacija. Moze da e prethodnik na napadi kako Brute-force ili API abuse.
#### Koristeni maliciozni aktivnosti: 
- API scan
- auth test
#### Preporaki: 
- monitoring na IP adresata
- ako ne e poznata da se razgleda blokiranje
- ogranicuvanje na API povici
- logiranje na neuspesni obidi
- proverka na parametri

## 203.0.113.42
Koristi python skripti, sto e najverojatno avtomatiziran bot, prebaruva .robots.txt i sitemap.xml, isto taka ima obidi za API manipulacija sto e somnitelno.
#### Koristeni maliciozni aktivnosti
- API scan
- baranje cuvstvitelni fajlovi
- avtomatizirano odnesuvanje
#### Preporaki: 
- monitoring na IP adresata
- ako ne e legitimna da se blokira
- ogranicuvanje na API povici
- logiranje na neuspesni obidi

## 104.16.248.131
Moze da e somnitelen, menuva user agents okhttp na mozilla, skenira API i blog, moze da e web scrapper, megjutoa mora da se proveri ako ne e negov accountot sto se logira e problem.
#### Preporaki: 
- monitoring na IP adresata
- ako ne e legitimna da se blokira
- proverka na logovi

# Zaklucok

## Spored mene, ovoj sajt e hakiran (lici na SETEC scenario malku), podatocite mozat da bidat zloupotrebeni i treba da se prevzemat itni merki za bezbednost kako sto e navedeno pogore
