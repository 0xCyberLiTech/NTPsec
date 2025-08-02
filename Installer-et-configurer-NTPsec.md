
<div align="center">
  
<br></br>
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ENTPsec_" alt="Titre dynamique NTPsec_" />
</a>
<br></br>

<p align="center">
  <em>Un dépôt pédagogique autour du monde linux DEBIAN.</em><br>
  <b>📘 Apprentissage – 🔐 Sécurité – 🧠 Compréhension</b>
</p>

[![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
[![Latest Release](https://img.shields.io/github/v/release/0xCyberLiTech/0xcyberlitech?label=version)](https://github.com/0xCyberLiTech/0xcyberlitech/releases/latest)
[![Changelog](https://img.shields.io/badge/📄%20CHANGELOG-0xcyberlitech-blue)](https://github.com/0xCyberLiTech/0xcyberlitech/blob/main/CHANGELOG.md)
[![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)

</div>

---

### 👨‍💻 **À propos de moi.**

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> 🎯 **Objectif :** proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" alt="Logo techno" width="300">
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt GitHub.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant NTPsec (Network Time Protocol Security).
> Il s’adresse aux passionnés, étudiants et professionnels souhaitant mieux comprendre les mécanismes de synchronisation temporelle sécurisée sur les systèmes informatiques, apprendre à installer, configurer et administrer NTPsec, ainsi qu’à se familiariser avec les bonnes pratiques et outils permettant d’assurer une précision optimale et une protection renforcée contre les attaques visant le protocole NTP.

---



---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
















## Installer et configurer NTPsec sur DEBIAN 12.

## NTPsec remet les pendules d’Internet à l’heure de la sécurité.

Le protocole NTP, maître du temps de l’Internet, est devenu vulnérable.

Un spécialiste de l’Open Source s’est attelé à son successeur NTPSec.

Retour vers le futur, la suite sur Internet ? Des chercheurs mettent en évidence les failles de NTP, le protocole de synchronisation des horloges d’Internet. Vulnérabilités qui ouvrent la porte à des attaques par DDoS, mais aussi à la mise en danger des communications chiffrées.

Dérégler l’horloge de l’Internet ? C’est en somme le tour de passe-passe que dévoilent des chercheurs dans un article : ce dernier met en exergue les failles du Network Time Protocol (NTP), le (très ancien) protocole de synchronisation qui permet de caler l’horloge locale d’ordinateurs sur une référence, un serveur présent sur le réseau. Or, ces connexions entre clients et serveurs sont en pratique rarement chiffrées – même si le protocole l’autorise – laissant la porte ouverte à des attaques de type Man-in-the-Middle où un serveur ‘pirate’ vient s’intercaler dans la communication. Une façon de modifier l’horloge des systèmes clients. Quelle importance pourrait-on penser en première approche, puisqu’il ne s’agit que d’une simple modification de l’heure ?

« NTP se cache en arrière-plan de bien des systèmes, écrivent les 4 chercheurs issus de l’université de Boston (Massachussetts). Quand NTP échoue sur un système, de nombreuses applications de ce système peuvent à leur tour planter, toutes en même temps ». Tout sauf de la science-fiction, ajoutent les auteurs de l’étude. En 2012, deux serveurs NTP de la marine américaine, la Navy, sont remontés dans le temps de 12 années, provoquant des pannes sur une multitude de systèmes, comme l’authentification Active Directory, des autocommutateurs ou des routeurs. Qui plus est, ce type d’attaques DDoS un peu originales peuvent être menées sans que l’assaillant ait à monitorer le trafic entre les clients et le serveur NTP.

## La faille Heartbleed reloaded :
C’est par exemple le cas de l’attaque dite du ‘baiser-de-la-mort’ (Kiss-o’-Death ou KoD), qui consiste à envoyer quelques paquets à chaque client NTP pour que ceux-ci cessent de demander la mise à jour de leur horloge. « Comme l’assaillant ne doit envoyer que quelques paquets à chaque victime, des outils de scan réseau standards (nmap, zmap) peuvent être adaptés pour lancer très rapidement l’attaque, en masse, sur la plupart des clients ntpd (le composant implémentant NTP, NDLR) présents sur Internet », explique Sharon Goldberg, un des chercheurs.

Au-delà de ces formes d’attaque visant à causer des interruptions de service ou des pannes, les chercheurs imaginent des scénarios d’attaque bien plus sophistiqués. Exemple avec les certificats TLS (utilisés pour le HTTPS) : en faisant monter des systèmes dans ‘la machine à remonter le temps’ du NTP, un assaillant peut les amener à accepter des certificats révoqués. Par exemple, en ramenant les horloges avant la mi-2014, époque où plus de 100 000 certificats TLS ont été rayés de la carte en raison de la faille Heartbleed. Même constat avec DNSSEC, le protocole qui fournit l’authentification sur les données DNS (Domain Name System, le système de correspondance entre URL et adresses IP). En se servant de la durée de vie très faible des certificats du DNSSEC, un assaillant peut, en utilisant NTP, faire tomber toutes les connexions aux domaines sécurisés par DNSSEC. Ces scénarios d’attaque, mariant manipulation de l’horloge et durée de vie des certificats, peuvent aussi être employés contre les services Cloud, comme Amazon S3 ou Dropbox. L’idée ? Se baser sur les limites d’horodatage que mettent en place ces services pour empêcher des accès non autorisés, pour barrer l’accès aux utilisateurs légitimes ou – justement – ménager des accès non autorisés en se projetant quelques minutes en arrière, au moment où une authentification devenue depuis obsolète était encore valide.

## Profiter du reboot pour faire un saut dans le temps :
Si ces scénarios sophistiqués sont évidemment inquiétants, reste à savoir s’ils sont utilisables en pratique. D’abord, un changement brutal dans l’horloge risque fort de provoquer des erreurs dans les systèmes d’exploitation ou les applications des clients ciblés. Rendant toute extraction de données illusoire. Ensuite, le protocole NTP prévoit normalement que les clients rejettent des modifications temporelles de plus de 1000 secondes (environ 16 minutes). Sauf que les chercheurs de l’université de Boston expliquent que deux méthodes permettent de contourner cette sécurité. D’abord, via une série de modifications de l’horloge, chacune inférieure à la limite prévue. Entre deux modifications, un intervalle de 5 minutes doit toutefois être respecté (sur ntpd v4.2.8). Conséquence : avancer ou reculer l’horloge d’un client d’un an prendrait… 114 jours ! Les chercheurs de l’université de Boston présentent donc une méthode plus efficace, exploitant la capacité des systèmes à accepter n’importe quel saut dans le temps au moment du reboot.

Certaines des attaques évoquées par les chercheurs ne surprendront pas les spécialistes. En août dernier, le chercheur Jose Delvi en présentait déjà certaines. Ce dernier a même réalisé un outil, un serveur NTP permettant de tester ces méthodes, baptisé Delorean en hommage à la voiture des voyages spatio-temporels du film Retour vers le futur. Jose Delvi a publié le 21 octobre 2015, le jour choisi par Marty McFly, le héros du film, pour son second voyage dans le futur, un billet de blog, dans lequel il fait le constat suivant : « tous les vendeurs d’OS que j’ai testés utilisent les Network Time Protocol (NTP) afin de garder les horloges internes à l’heure juste, ce qui est très important pour certains protocoles d’authentification notamment. La plupart d’entre eux ne déploient pas ce service de façon sécurisée, le rendant vulnérable à des attaques de type Man-in-the-Middle ».

## Amplificateur de DDoS :
De leur côté, les chercheurs de l’université de Boston ont publié une page de diagnostic et de recommandations concernant tant les serveurs que les clients NTP. Ils recommandent notamment l’usage de NTP v4.2.8p4 (qui élimine le KoD) ainsi que diverses autres options de configuration censées limiter la portée ou la variété des attaques possibles contre le protocole.

Notons que la vulnérabilité de NTP avait également été mise en évidence début 2014, quand des assaillants avaient utilisé le protocole pour amplifier une attaque DDoS contre des sites de jeu en ligne. Une requête aux serveurs NTP semblant émaner de ces sites renvoyait un message jusqu’à 58 fois plus volumineux, décuplant ainsi les capacités des assaillants et saturant les systèmes ciblés.

## Installez et configurer (NTPsec).
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
restrict ::1 nomodify
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
Un moyen simple de voir s'il y a un broadcast NTP dans votre réseau local (généralement le router) :

N'oublier pas d'installer le paquet tcpdump :
```
apt install tcpdump -y
```
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
Info complémentaire sur les restrictions de contrôle d'accès par défaut:

La ligne suivante définit les restrictions de contrôle d'accès par défaut :
```
restrict default nomodify notrap nopeer noquery
```
Les options nomodify empêchent tout changement de configuration.

- L'option notrap empêche les interruptions de protocole de messages de contrôle ntpdc.
- L'option nopeer empêche la formation d'association de pairs.
- L'option noquery empêche de répondre aux requêtes ntpq et ntpdc, mais n'empêche pas de répondre aux requêtes de temps.

---

Merci pour ta visite — et bon déploiement Debian ! 💻🚀

---

<p align="center">
  🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour une cybersécurité accessible à tous.
</p>
