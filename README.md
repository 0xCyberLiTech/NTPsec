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
> [!TIP]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Guide de Lecture &amp; Progression par Niveau (NTPsec)**
> - **Rôle de la brique :** **NTPsec / Chrony** maintient la synchronisation horaire de haute précision (hiérarchie **Stratum 1 à 4**) sur l'ensemble des serveurs et équipements réseau, condition indispensable à la validité des certificats TLS, des jetons d'authentification et de la corrélation forensique des journaux.
> - **Parcours recommandé :** **Niveau 1 (Fondamentaux &amp; Installation initiale)** pour déployer une base saine &rarr; **Niveau 2 (Configuration &amp; Intégration)** &rarr; **Niveau 3 (Haute Disponibilité, Durcissement &amp; Exploitation)**.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **NTPsec / Chrony** maintient la synchronisation horaire de haute précision (hiérarchie **Stratum 1 à 4**) sur l'ensemble des serveurs et équipements réseau, condition indispensable à la validité des certificats TLS, des jetons d'authentification et de la corrélation forensique des journaux.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports IANA :** `UDP 123` (NTP) · `TCP 4460` (NTS-KE — *Network Time Security*) &nbsp;|&nbsp; **Fichier Debian :** `/etc/ntpsec/ntp.conf` &nbsp;|&nbsp; **Validation officielle :** `ntpq -p` et `timedatectl timesync-status`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Dans la table `ntpq -p`, le préfixe **`*`** identifie la source horaire maîtresse active (*sys.peer*), le préfixe **`+`** indique les serveurs candidats de secours, et une valeur `reach` bloquée à `0` signale un filtrage du port `UDP 123`. Le niveau de **Stratum** indique la distance par rapport à l'horloge atomique ou GPS de référence (Stratum 0).
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle NTPsec](https://docs.ntpsec.org/latest/) &nbsp;·&nbsp; [RFC 5905 (NTPv4) & RFC 8915 (NTS)](https://datatracker.ietf.org/doc/html/rfc8915)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // SOMMAIRE DES DOSSIERS TECHNIQUES — ATELIER NTPSEC // HORLOGE ATOMIQUE
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<div align="center">

|  **Catégorie** | *Description**         |  **Accès rapide**                                                                                                                              |
|----------------|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **NTPsec**     | Installer et configure | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](Installer-et-configurer-NTPsec.md) |

</div>

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
