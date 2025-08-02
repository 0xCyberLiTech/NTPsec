
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


## 📚 Installer et configurer **NTPsec** sur Debian 12  
**Synchronisation horaire sécurisée pour protéger vos systèmes**  

---

### 🕒 Pourquoi remplacer NTP par NTPsec ?  

Le protocole **NTP** (Network Time Protocol) est depuis longtemps l’horloge de référence d’Internet.  
Cependant, il est ancien, peu sécurisé dans ses implémentations classiques et a fait l’objet de nombreuses vulnérabilités :  
- **Attaques DDoS amplifiées** via serveurs NTP mal configurés.  
- **Manipulation de l’heure système** pouvant invalider des mécanismes de sécurité.  
- **Attaques Man-in-the-Middle** facilitée par l’absence de chiffrement dans la majorité des déploiements.  

**NTPsec** est une version sécurisée et allégée de NTP, conçue pour corriger ces failles et limiter la surface d’attaque.  
Il est développé en Open Source avec un code modernisé et audité.  

---

### 🚨 Exemple de risques liés à un NTP non sécurisé  

- **Défaillances en chaîne** : en 2012, deux serveurs NTP de la marine américaine ont reculé de **12 ans** →  
  → pannes massives (Active Directory, téléphonie IP, routeurs).  
- **Acceptation de certificats TLS révoqués** : en ajustant l’heure en arrière, un attaquant peut faire croire qu’un certificat expiré est encore valide (*exemple : Heartbleed en 2014*).  
- **Perturbation de DNSSEC** : horodatages erronés → impossibilité de résoudre certains domaines sécurisés.  
- **Exploitation en DDoS** : amplification jusqu’à ×58 du trafic, saturant les réseaux cibles.  

---

### 🔐 Avantages de NTPsec  

- Code source réduit de 75 % par rapport à ntpd classique (moins de bugs potentiels).  
- Suppression de fonctionnalités obsolètes et vulnérables (ex. : KoD - Kiss-o’-Death).  
- Meilleure gestion des restrictions et du contrôle d’accès.  
- Support natif du chiffrement (*Network Time Security - NTS*).  

---

## 🛠 Installation de NTPsec sur Debian 12  

```bash
sudo apt update && sudo apt -y install ntpsec
```

---

## ⚙️ Configuration de base  

Éditer le fichier de configuration :  
```bash
sudo nano /etc/ntpsec/ntp.conf
```

🔹 **Remplacer les serveurs par défaut** par ceux de votre pays/fuseau horaire :  
```conf
#pool 0.debian.pool.ntp.org iburst
#pool 1.debian.pool.ntp.org iburst
#pool 2.debian.pool.ntp.org iburst
#pool 3.debian.pool.ntp.org iburst

pool 0.fr.pool.ntp.org iburst
pool 1.fr.pool.ntp.org iburst
pool 2.fr.pool.ntp.org iburst
pool 3.fr.pool.ntp.org iburst
```

---

### 🔒 Restreindre les accès NTP  

En fin de fichier `ntp.conf` :  
```conf
restrict default kod notrap nomodify nopeer noquery
restrict 127.0.0.1 nomodify
restrict ::1 nomodify
restrict 10.8.0.0 mask 255.255.255.0 nomodify notrap
restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap
```

Redémarrer le service :  
```bash
sudo systemctl restart ntpsec.service
```

---

### 📊 Vérifier la synchronisation  

```bash
ntpq -p
```

Exemple de sortie :  
```
     remote           refid      st t when poll reach   delay   offset   jitter
===============================================================================
 0.fr.pool.ntp.org   .POOL.      16 p    -  256    0   0.0000   0.0000   0.0001
 1.fr.pool.ntp.org   .POOL.      16 p    -  256    0   0.0000   0.0000   0.0001
```

---

### 📡 Diagnostic réseau NTP  

Vérifier les diffusions NTP locales :  
```bash
sudo apt install tcpdump -y
sudo tcpdump -n "broadcast or multicast" | grep NTP
```

Lister les clients connectés à votre serveur NTP :  
```bash
ntpq -c mrulist
```

---

### ⚠️ Note de sécurité  

- **Ne jamais** retirer `noquery` sur un serveur NTP public → risque d’amplification DDoS.  
- Voir la vulnérabilité **CVE-2013-5211** pour plus de détails.  
- Autoriser explicitement l’accès local :  
```conf
restrict 127.0.0.1
restrict ::1
```

---

📎 **Sources et recommandations** :  
- [Site officiel NTPsec](https://ntpsec.org)  
- [Best Practices NTPsec](https://docs.ntpsec.org/latest/)  
- [Recommandations de sécurité CERT](https://www.cisa.gov)  

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
