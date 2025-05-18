1. Направете пасивен scan на доменот beyondmachines.net, и пронајдете колку DNS записи за сервери има во него. Колку од нив се активни, колку ви изгледаат како заборавени или ранливи.
Можете да користите алатки како amass, subfinder, sublist3r, DNSrecon (не мора сите :) ). Не се обидувајте активно да скенирате, тоа одзема многу време. Спремете си белешки или список за на интервјуто: 
како ги баравте, што најдовте, каде се хостираат (барем од whois проверка), што по вас не би требало да е online.

# DNS_scan_report za beyondmachines.net

-------

## Koristeni alatki i resursi:

- [`amass`](https://github.com/owasp-amass/amass) – Passive subdomain enumeration
- [`subfinder`](https://github.com/projectdiscovery/subfinder) – Fast passive subdomain discovery
- [`sublist3r`](https://github.com/aboul3la/Sublist3r) – Subdomain enumeration using search engines
- [`nmap`](https://nmap.org/) – Port scanning and host discovery
- [`dnsrecon`](https://github.com/darkoperator/dnsrecon) – DNS enumeration and zone transfer testing
- [`curl`](https://curl.se/) – HTTP header inspection via CLI (`curl -I`)

- Online sources:
  - [crt.sh](https://crt.sh) – Subdomains from SSL certificate transparency logs
  - [WHOIS](https://who.is/) – Domain ownership and registration info
  - [`DIG`](https://linux.die.net/man/1/dig) – DNS record lookups
  - [`WhatWeb`](https://github.com/urbanadventurer/WhatWeb) – Fingerprinting web technologies
  - [DNSDumpster](https://dnsdumpster.com) – DNS records and subdomain mapping
  - [`Waybackurls`](https://github.com/tomnomnom/waybackurls) – Archived URLs from the Wayback Machine
  - [SecurityTrails](https://securitytrails.com/) – Passive DNS, subdomain, and DNS record data (API used)

-------

## Kako gi barav:

- Prvo napraviv scan so amass kaj sto dobiv detali za site subdomains na beyondmachines.net
##### amass enum -passive -d beyondmachines.net -o amass_results.txt -timeout 5

- potoa napraviv uste eden scan so subfinder
##### subfinder -d beyondmachines.net -o subfinder_results.txt

- gi spoiv rezultatite i gi filtrirav so sort i uniq
##### cat ~/Downloads/amass_Linux_amd64/amass_results.txt subfinder_results.txt | sort | uniq > all_subdomains.txt

- kaj sto mi dade 13 rezultati so subdomains vo datotekata all_subdomains.txt

- da se osiguram skinirav i so sublist3r
##### python3 sublist3r.py -d beyondmachines.net -o subdomains.txt

- posle so nmap go skenirav dokumentot, koj isto taka mi dade isto taka 13 rezultati so istite zapisi kako i subfinder i amass
##### nmap -iL subdomains.txt -T4 -F -Pn

- istite se naogjaat i na linkot za SSL/TLS sertifikati kaj sto proveriv dali se validni i gi ima
##### https://crt.sh/?q=%25.beyondmachines.net


### Aktivni - 5 - (proverka so dig, curl, whatweb, whois ...)

###### www.beyondmachines.net (18.244.87.20) - host AWS

###### challenge.beyondmachines.net (185.199.111.153) - host GITHUB
Treba da bide aktivna samo dodeka trae challenge-ot, last modified e pred 4 meseci, deluva na zaboravena, nema potreba da bide izlozena na dopolnitelen rizik i pogolema povrsina za napad, moze da se avtomatizira next challenge, da se ukradat informacii etc..

###### old.beyondmachines.net (192.0.78.189) - host AUTOMATTIC
I ovaa nema potreba da bide aktivna, pokazuva na wordpress, unrelated e, dokolku vlece nekoi stari podatoci sto trebaat momentalno, okej, dokolku ne vlece i ne se koristi za nisto, treba da bide trgnata zasto 
moze da se najde star kontent, netocen kontent, stari passwordi, emails etc. Ili ako mora da e aktivna treba da pokaze 404, last updated vo 2024...

###### trust.beyondmachines.net (104.18.5.130) - host CLOUDFLARE
Moze da bide aktivna samo ako sluzi za legalni informacii ili privacy policy, vo sprotivno nema potreba, kako uste da e vo produkcija i da ne e zavrsena mi deluva. Isto vrakja 403 forbidden error sto e somnitelno od terminal,
znaci ne moze da bide proverena, sto e dobar znak za security i ima jaki security headers.

###### yieldcat.beyondmachines.net (216.24.57.1) - host CLOUDFLARE
Moze da bide aktiven ako se sluzi za testiranje ili ucenje, izgleda safe, moze da bide potencijalen kandidat za napad ako ne e pravilno osigurana i odrzuvana.


### Neaktivni - 8 - (proverka so dig, curl, whatweb, whois ...)

###### ako.beyondmachines.net
###### clarity.beyondmachines.net
###### damascian.beyondmachines.net
###### damascian-online.beyondmachines.net
###### rendertest.beyondmachines.net
###### status.beyondmachines.net
###### testalb.beyondmachines.net
###### yieldhog.beyondmachines.net

#### od neaktivnite - nema potencijalno nisto
bi trebalo da se izbrisat site DNS na neaktivnite, mora i da se iscistat site DNS zapisi za da ne moze nekoja budala samo so kreiranje na novo repo ili bucket da go prevzeme domainot
moze da se iskoristat za da se napravi github repo so istoto ime i da se ima kontrola na toj domain, da se napravi takeover na domainot

## Ne mislev deka samo tie zapisi moze da se najdat, istrazuvav uste i so nekoi drugi alatki pronajdov uste 4, od koi 3 se aktivni, 1 ne e aktiven. koristev dnsx - so wordlist, dnsumpster, waybackurls, securitytrails - API

### Drugi - 4

###### app.beyondmachines.net (18.244.87.78) host AWS
ne znaev zasto se koristi, ista ip adresa, dali e zaboravena ili se koristi za develop, moze da e okej da se ima 2 isti, megjutoa moze da se napravi problem
ako edna od dvete imaat poslabi security headers ili poslaba konfiguracija, stanuva weak point, isto taka povekje DNS zapisi se odrzuvaat, ako e aplikacija i se koristi kako main site moze da se zbunat korisnicite i developerite.
ako se koristi treba da ima isti konfiguracii kako glavnata strana ili pa da se napravi redirect do taa

###### workshop.beyondmachines.net (18.165.72.99) host AWS
ova izgleda kako zaboraveno sto isto taka nema potreba da e online dodeka ne trae, workshopot se odrzal, pogolema povrsina za napad, moze da se zloupotrebat podatoci

###### pubcdn.beyondmachines.net (18.165.72.104) host AWS
nikako ne smee da bide aktivna ako ne se koristi, vrakja 403 error sto e somnitelno, dzabe pogolema povrsina za napad...
treba da se izbrise DNS recordot, da se deaktivira cloudfront ako ne se koristi.

###### test.beyondmachines.net
ne e aktiven, isto taka ne mozam da najdam nisto, bi trebalo da e ok ako e izbrisan sekoj DNS zapis

# Istrazuvanja

### Testiranje so DNS recon
- DNS transferite se dobro konfigurirani
- Email security ne e kompletno, SPF i DMARC gi ima, megjutoa DMARC p=none
- Ima nekoi subdomains sto se nepotrebno izlozeni na rizik

# Preporaki

- Treba da se izbrisat ili da se iskoristat pravilno site subdomains sto deluvaat kako izbrisani ili zaboraveni
- Tie sto se za testiranje ili ucenje da se obrne pogolemo vnimanie okolu security zasto e golem rizik
- Da se update DMARC p=none vo p=reject ili p=quarantine za da ima pogolema zastita na email spoofing
- redirect na duplikati kako app.beyondmachines.net subdomains do main site ako ne trebaat
- da se obezbedi dobro sekoj subdomain so security headers, HTTPS, CSP
- sekogas dobro da se sledi koj subdomains se vo upotreba
- da ne se ostavaat zastareni DNS zapisi
