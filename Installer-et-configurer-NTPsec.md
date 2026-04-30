<div align="center">
  
  <br></br>

  </p>
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ENTPsec_" alt="Titre dynamique NTPsec_" />
  </a>

  <br></br>
  
  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>

  <p align="center">
    <a href="https://0xcyberlitech.github.io/">
      <img src="https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square" alt="Portfolio" />
    </a>
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="Profil GitHub" />
    </a>
    <a href="https://github.com/0xCyberLiTech/NTPsec/releases/latest">
      <img src="https://img.shields.io/github/v/release/0xCyberLiTech/NTPsec?label=version" alt="Latest Release" />
    </a>
    <a href="https://github.com/0xCyberLiTech/NTPsec/blob/main/CHANGELOG.md">
      <img src="https://img.shields.io/badge/📄%20CHANGELOG-NTPsec-blue" alt="Changelog" />
    </a>
    <a href="https://github.com/0xCyberLiTech?tab=repositories">
      <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="Dépôts publics" />
    </a>

</div>

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

<div align="center">
  
## À propos & Objectifs.

</div>

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

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

<div align="center">

<table>
<tr>
<td align="center"><b>🖥️ Infrastructure &amp; Sécurité</b></td>
<td align="center"><b>💻 Développement &amp; Web</b></td>
<td align="center"><b>🤖 Intelligence Artificielle</b></td>
</tr>
<tr>
<td align="center">
  <a href="https://www.kernel.org/"><img src="https://skillicons.dev/icons?i=linux" width="48" title="Linux" /></a>
  <a href="https://www.debian.org"><img src="https://skillicons.dev/icons?i=debian" width="48" title="Debian" /></a>
  <a href="https://www.gnu.org/software/bash/"><img src="https://skillicons.dev/icons?i=bash" width="48" title="Bash" /></a>
  <br/>
  <a href="https://nginx.org"><img src="https://skillicons.dev/icons?i=nginx" width="48" title="Nginx" /></a>
  <a href="https://www.docker.com"><img src="https://skillicons.dev/icons?i=docker" width="48" title="Docker" /></a>
  <a href="https://git-scm.com"><img src="https://skillicons.dev/icons?i=git" width="48" title="Git" /></a>
</td>
<td align="center">
  <a href="https://www.python.org"><img src="https://skillicons.dev/icons?i=python" width="48" title="Python" /></a>
  <a href="https://flask.palletsprojects.com"><img src="https://skillicons.dev/icons?i=flask" width="48" title="Flask" /></a>
  <a href="https://developer.mozilla.org/docs/Web/HTML"><img src="https://skillicons.dev/icons?i=html" width="48" title="HTML5" /></a>
  <br/>
  <a href="https://developer.mozilla.org/docs/Web/CSS"><img src="https://skillicons.dev/icons?i=css" width="48" title="CSS3" /></a>
  <a href="https://developer.mozilla.org/docs/Web/JavaScript"><img src="https://skillicons.dev/icons?i=js" width="48" title="JavaScript" /></a>
  <a href="https://code.visualstudio.com"><img src="https://skillicons.dev/icons?i=vscode" width="48" title="VS Code" /></a>
</td>
<td align="center">
  <a href="https://pytorch.org"><img src="https://skillicons.dev/icons?i=pytorch" width="48" title="PyTorch" /></a>
  <a href="https://www.tensorflow.org"><img src="https://skillicons.dev/icons?i=tensorflow" width="48" title="TensorFlow" /></a>
  <a href="https://www.raspberrypi.com"><img src="https://skillicons.dev/icons?i=raspberrypi" width="48" title="Raspberry Pi" /></a>
  <br/><br/>
  <a href="https://ollama.com"><img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama" /></a>
  &nbsp;
  <a href="https://anthropic.com"><img src="https://img.shields.io/badge/Anthropic-D97757?style=for-the-badge&logo=anthropic&logoColor=white" alt="Anthropic" /></a>
</td>
</tr>
</table>

<br/>

<b>🔒 Un projet proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Développé en collaboration avec <a href="https://claude.ai">Claude AI</a> (Anthropic) 🔒</b>

</div>

