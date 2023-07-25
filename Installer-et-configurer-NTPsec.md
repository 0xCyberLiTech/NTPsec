<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-ntpsec.svg" alt="ATELIER NTPSEC // HORLOGE ATOMIQUE" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`ntpsec`) :** `Bookworm (12)` : **`1.2.2+dfsg1-1+deb12u1`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`1.2.3+dfsg1-8`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`1.2.5+dfsg-1`**
> - **Références Officielles :** [Paquet Debian Trixie (`ntpsec`)](https://packages.debian.org/trixie/ntpsec) &nbsp;·&nbsp; [Paquet Debian Forky (`ntpsec`)](https://packages.debian.org/forky/ntpsec) &nbsp;·&nbsp; [Documentation Officielle Debian](https://manpages.debian.org/trixie/ntpsec/ntpd.8.en.html)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Depuis Debian 12/13 (Trixie) et sous Debian 14 (Forky), le paquet `ntp` historique est remplacé par **`ntpsec`** (fichier de configuration `/etc/ntpsec/ntp.conf` et service `ntpsec.service`).

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie) — NTPsec a remplace le vieux paquet 'ntp' historique :
sudo apt update && sudo apt install -y ntpsec
ntpq -p && sudo systemctl status ntpsec
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Configuration dans /etc/ntpsec/ntp.conf & suivi journald :
sudo journalctl -u ntpsec.service -n 30 --no-hostname
ntptime
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **NTPsec / Chrony** maintient la synchronisation horaire de haute précision (hiérarchie **Stratum 1 à 4**) sur l'ensemble des serveurs et équipements réseau, condition indispensable à la validité des certificats TLS, des jetons d'authentification et de la corrélation forensique des journaux.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports IANA :** `UDP 123` (NTP) · `TCP 4460` (NTS-KE — *Network Time Security*) &nbsp;|&nbsp; **Fichier Debian :** `/etc/ntpsec/ntp.conf` &nbsp;|&nbsp; **Validation officielle :** `ntpq -p` et `timedatectl timesync-status`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Dans la table `ntpq -p`, le préfixe **`*`** identifie la source horaire maîtresse active (*sys.peer*), le préfixe **`+`** indique les serveurs candidats de secours, et une valeur `reach` bloquée à `0` signale un filtrage du port `UDP 123`. Le niveau de **Stratum** indique la distance par rapport à l'horloge atomique ou GPS de référence (Stratum 0).
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle NTPsec](https://docs.ntpsec.org/latest/) &nbsp;·&nbsp; [RFC 5905 (NTPv4) & RFC 8915 (NTS)](https://datatracker.ietf.org/doc/html/rfc8915)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Installer et configurer **NTPsec** sur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky)<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
**Synchronisation horaire sécurisée pour protéger vos systèmes**  

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Pourquoi remplacer NTP par NTPsec ?

Le protocole **NTP** (Network Time Protocol) est depuis longtemps l’horloge de référence d’Internet.  
Cependant, il est ancien, peu sécurisé dans ses implémentations classiques et a fait l’objet de nombreuses vulnérabilités :  
- **Attaques DDoS amplifiées** via serveurs NTP mal configurés.  
- **Manipulation de l’heure système** pouvant invalider des mécanismes de sécurité.  
- **Attaques Man-in-the-Middle** facilitée par l’absence de chiffrement dans la majorité des déploiements.  

**NTPsec** est une version sécurisée et allégée de NTP, conçue pour corriger ces failles et limiter la surface d’attaque.  
Il est développé en Open Source avec un code modernisé et audité.  

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-threat.svg" width="18" height="18" align="absmiddle" alt="" /> Exemple de risques liés à un NTP non sécurisé

- **Défaillances en chaîne** : en 2012, deux serveurs NTP de la marine américaine ont reculé de **12 ans** →  
  → pannes massives (Active Directory, téléphonie IP, routeurs).  
- **Acceptation de certificats TLS révoqués** : en ajustant l’heure en arrière, un attaquant peut faire croire qu’un certificat expiré est encore valide (*exemple : Heartbleed en 2014*).  
- **Perturbation de DNSSEC** : horodatages erronés → impossibilité de résoudre certains domaines sécurisés.  
- **Exploitation en DDoS** : amplification jusqu’à ×58 du trafic, saturant les réseaux cibles.  

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> Avantages de NTPsec

- Code source réduit de 75 % par rapport à ntpd classique (moins de bugs potentiels).  
- Suppression de fonctionnalités obsolètes et vulnérables (ex. : KoD - Kiss-o’-Death).  
- Meilleure gestion des restrictions et du contrôle d’accès.  
- Support natif du chiffrement (*Network Time Security - NTS*).  

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Installation de NTPsec sur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky)<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt -y install ntpsec
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Configuration de base
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Éditer le fichier de configuration :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo nano /etc/ntpsec/ntp.conf
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Remplacer les serveurs par défaut** par ceux de votre pays/fuseau horaire : 

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> #pool 0.debian.pool.ntp.org iburst
> #pool 1.debian.pool.ntp.org iburst
> #pool 2.debian.pool.ntp.org iburst
> #pool 3.debian.pool.ntp.org iburst
>
> pool 0.fr.pool.ntp.org iburst
> pool 1.fr.pool.ntp.org iburst
> pool 2.fr.pool.ntp.org iburst
> pool 3.fr.pool.ntp.org iburst
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> Restreindre les accès NTP

En fin de fichier `ntp.conf` :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> restrict default kod notrap nomodify nopeer noquery
> restrict 127.0.0.1 nomodify
> restrict ::1 nomodify
> restrict 10.8.0.0 mask 255.255.255.0 nomodify notrap
> restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap
> ```
<!-- CODE-WINDOW-END -->

Redémarrer le service :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl restart ntpsec.service
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Vérifier la synchronisation

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ntpq -p
> ```
<!-- CODE-WINDOW-END -->

Exemple de sortie :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>      remote           refid      st t when poll reach   delay   offset   jitter
> ===============================================================================
>  0.fr.pool.ntp.org   .POOL.      16 p    -  256    0   0.0000   0.0000   0.0001
>  1.fr.pool.ntp.org   .POOL.      16 p    -  256    0   0.0000   0.0000   0.0001
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-network.svg" width="18" height="18" align="absmiddle" alt="" /> Diagnostic réseau NTP

Vérifier les diffusions NTP locales :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt install tcpdump -y
> sudo tcpdump -n "broadcast or multicast" | grep NTP
> ```
<!-- CODE-WINDOW-END -->

Lister les clients connectés à votre serveur NTP :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ntpq -c mrulist
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> Note de sécurité

- **Ne jamais** retirer `noquery` sur un serveur NTP public → risque d’amplification DDoS.  
- Voir la vulnérabilité **CVE-2013-5211** pour plus de détails.  
- Autoriser explicitement l’accès local :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> restrict 127.0.0.1
> restrict ::1
> ```
<!-- CODE-WINDOW-END -->

---

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Sources et recommandations** : 
- [Site officiel NTPsec](https://ntpsec.org)  
- [Best Practices NTPsec](https://docs.ntpsec.org/latest/)  
- [Recommandations de sécurité CERT](https://www.cisa.gov)  

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
