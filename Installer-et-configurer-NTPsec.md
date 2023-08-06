## Installer et configurer NTP Server (NTPsec) sur DEBIAN 12.

Installez et configurer (NTPsec).

NTP utilise le port 123 en UDP.

Recalibrer la time zone :
```
dpkg-reconfigure tzdata
```
```
Current default time zone: 'Europe/Paris'
Local time is now:      Tue Jul 25 14:35:59 CEST 2023.
Universal Time is now:  Tue Jul 25 12:35:59 UTC 2023.
```
```
apt -y install ntpsec
```
```
nano /etc/ntpsec/ntp.conf
```
Commentez les paramètres par défaut et ajoutez des serveurs NTP pour votre fuseau horaire :
```
#pool 0.debian.pool.ntp.org iburst
#pool 1.debian.pool.ntp.org iburst
#pool 2.debian.pool.ntp.org iburst
#pool 3.debian.pool.ntp.org iburst
```
```
pool 0.fr.pool.ntp.org iburst
pool 1.fr.pool.ntp.org iburst
pool 2.fr.pool.ntp.org iburst
pool 3.fr.pool.ntp.org iburst
```
Apporter des restrictions sur votre réseau.

À la fin du fichier de configuration rajouter ce-ci :

Vous pouvez restreindre les clients (les ordinateurs autorisés à synchroniser leur horloge sur le serveur) :
```
restrict default kod notrap nomodify nopeer noquery
restrict 127.0.0.1 nomodify
restrict ::1
restrict 10.8.0.0 mask 255.255.255.0 nomodify notrap
restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap
```
```
systemctl restart ntpsec.service
```
Vérifier le statut de NTPsec.
```
ntpq -p
```
```
     remote                                   refid      st t when poll reach   delay   offset   jitter
=======================================================================================================
 0.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 1.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 2.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 3.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
```
Un moyen simple de voir s'il y a un broadcast NTP dans votre réseau local (généralement le router):
```
sudo tcpdump -n "broadcast or multicast" | grep NTP
```
Pour voir si des clients se connectent à votre serveur NTP :
```
ntpq -c mrulist
```
Note sécurié :

Important :

Les requêtes ntpq et ntpdc peuvent être utilisées dans les attaques d'amplification, veuillez donc ne pas supprimer l'option noquery de la commande restrict default sur des systèmes accessibles publiquement.

Veuillez consulter CVE-2013-5211 pour obtenir davantage de détails.

Les adresses situées dans la plage 127.0.0.0/8 sont parfois requises par divers processus ou applications.

Comme la ligne « restrict default » (restreindre par défaut) ci-dessus prévient l'accès à tout ce qui n'est pas explicitement autorisé, l'accès à l'adresse de bouclage IPv4 et IPv6 est autorisé au moyen des lignes suivantes :

```
# the administrative functions.
restrict 127.0.0.1
restrict ::1
```
