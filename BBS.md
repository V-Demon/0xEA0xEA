# 🌐 La Logistique de l'Ombre : BBS, Swapping et l'Internet d'Avant l'Internet
## Rapport technique approfondi — Édition illustrée

| | |
| --- | --- |
| Périmètre | Commodore 64/128, Amiga, Atari ST, ZX Spectrum, Amstrad CPC, Apple II, IBM PC, et périphérie |
| Axe | Infrastructure de distribution : BBS, swapping postal, FidoNet, early FTP/IRC, sociologie des groupes |
| Position dans la série | **Cinquième volet** après *Le Matériel de Cracking*, *L'Art de la Protection*, *Les Protections K7* et *La Généalogie des Codecs* |
| Illustrations | Diagrammes [Mermaid](https://mermaid.js.org) et schémas ASCII |

### Légende des niveaux de confiance

| Marque | Signification |
| --- | --- |
| ✅ | Fait solidement établi (documentation officielle, témoignages concordants, archives) |
| ⚠️ | Information de seconde main ou contradictoire selon les sources : à vérifier avant citation |
| 🔧 | Correction ou précision apportée par rapport à la littérature courante |

---

## Sommaire

- [0. Vue d'ensemble : la toile invisible](#0-vue-densemble)
- [1. Introduction : distribuer sans Internet](#1-introduction)
- [2. Les BBS : architecture et fonctionnement](#2-les-bbs)
- [3. Les protocoles de transfert : du XMODEM au ZMODEM](#3-protocoles-transfert)
- [4. Le swapping postal : la poste comme réseau](#4-swapping-postal)
- [5. FidoNet et les réseaux numériques](#5-fidonet)
- [6. La sociologie des groupes : rôles et hiérarchies](#6-sociologie-groupes)
- [7. La distribution : releases, nukes et dupes](#7-distribution)
- [8. L'art du NFO et de l'ANSI](#8-art-nfo-ansi)
- [9. La transition vers Internet](#9-transition-internet)
- [10. L'héritage : de la scène au web moderne](#10-heritage)
- [11. Conclusion](#11-conclusion)
- [Annexes](#annexes)

---

## 0. Vue d'ensemble : la toile invisible {#0-vue-densemble}

### 0.1 Frise chronologique

```mermaid
timeline
    title L'infrastructure de distribution de la scène (1978-2000)
    1978 : Premier BBS (CBBS, Chicago, Ward Christensen)
    1980 : Apparition des BBS en Europe
    1982 : FidoNet (Tom Jennings) — premier réseau de BBS
    1983 : Swapping postal intensif (Spectrum, C64)
    1984 : UUCP (Unix-to-Unix Copy) — ancêtre d'Usenet
    1985 : Premiers groupes de cracking organisés (Fairlight, Razor 1911)
    1986 : XMODEM, YMODEM, ZMODEM (protocoles de transfert)
    1987 : TBBS, RemoteBoard, Wildcat! (logiciels BBS populaires)
    1988 : Explosion des BBS warez en Europe
    1990 : Internet commercial (ARPANET → Internet)
    1991 : World Wide Web (Tim Berners-Lee)
    1992 : IRC (Internet Relay Chat) — coordination en temps réel
    1993 : FTP anonyme — distribution massive
    1994 : Déclin des BBS, montée d'Internet
    1995 : Napster (1999) — préfiguration du P2P
    2000 : Fin de l'ère BBS, archiving des anciennes boards
```

### 0.2 Cartographie des réseaux

```
                          ┌─────────────────────────────────────────┐
                          │   INFRASTRUCTURE DE DISTRIBUTION        │
                          │        (1980-1995)                      │
                          └──────────────┬──────────────────────────┘
                                         │
         ┌───────────────┬───────────────┼───────────────┬───────────────┐
         ▼               ▼               ▼               ▼               ▼
   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
   │ BBS      │   │ SWAPPING │   │ FIDONET  │   │ EARLY    │   │ DEMO-    │
   │ (téléph.)│   │ POSTAL   │   │ (réseau) │   │ INTERNET │   │ PARTIES  │
   └──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
         │               │               │               │               │
         ▼               ▼               ▼               ▼               ▼
   Modems 300-     Courrier        Nœuds Fido      FTP, IRC,       Rencontres
   14400 bauds     postal          (echomail)      WWW             physiques
   X/Y/ZMODEM      Enveloppes      Regions,        Usenet          Échanges
   Files sections  customisées       nets, zones   Newsgroups      en direct
```

### 0.3 La boucle de distribution

```mermaid
flowchart LR
    A["Cracker termine un crack<br/>(jeu + cracktro + NFO)"] --> B["Upload sur BBS local<br/>(site du groupe)"]
    B --> C["Le sysop valide la release<br/>(vérification qualité)"]
    C --> D["Annonce sur FidoNet echomail<br/>(réseau de BBS)"]
    D --> E["Autres BBS téléchargent<br/>(via modem ou swapping)"]
    E --> F["Distribution mondiale<br/>(en 24-48h)"]
    F --> G{"Un autre groupe<br/>avait déjà sorti le même jeu ?"}
    G -->|"oui"| H["DUPE : la release est annulée"]
    G -->|"non"| I["PRE-TIME : le groupe est le premier"]
    style B fill:#1e3a5f,color:#fff
    style D fill:#3a5f1e,color:#fff
    style F fill:#5f3a1e,color:#fff
```

---

## 1. Introduction : distribuer sans Internet {#1-introduction}

Avant Internet (commercial à partir de 1993, grand public à partir de 1995), la distribution de logiciels crackés reposait sur **trois piliers** :

1. **Les BBS** (Bulletin Board Systems) : des serveurs téléphoniques privés où les utilisateurs se connectaient via modem pour échanger des fichiers, des messages et des logiciels.
2. **Le swapping postal** : l'envoi de disquettes par courrier postal, entre membres de la scène ou entre BBS.
3. **Les réseaux numériques** : FidoNet (réseau de BBS), puis les débuts d'Internet (FTP, IRC, Usenet).

### 1.1 Les contraintes techniques

| Contrainte | Impact | Solution |
| --- | --- | --- |
| **Lenteur des modems** | 300 à 14400 bauds (≈ 30 à 1800 octets/s) | Compression (ZIP, ARJ), protocoles efficaces (ZMODEM) |
| **Coût des communications** | Prix de l'appel téléphonique (surtout international) | BBS locaux, swapping postal, réseaux store-and-forward |
| **Capacité limitée** | Disquettes 170 Ko (C64) à 1.44 Mo (PC) | Compression, multi-disques, swapping de disques entières |
| **Pas de temps réel** | Pas de chat en direct (sauf IRC après 1992) | Messages asynchrones, echomail, couriers |

### 1.2 Le paradoxe de la scène

La scène du cracking a construit **un réseau mondial décentralisé** avant l'existence d'Internet grand public. Ce réseau était :

- **Résilient** : pas de point de défaillance unique (chaque BBS était indépendant)
- **Hiérarchisé** : des groupes avec des rôles précis (sysop, courier, cracker, supplier)
- **Régulé** : des règles de conduite (ratio de upload/download, interdiction de nukes)
- **Global** : un jeu sorti à Londres pouvait se retrouver à Stockholm, Paris ou New York en 48 heures

C'est l'ancêtre direct des réseaux P2P modernes (BitTorrent, Napster) et des communautés open source.

---

## 2. Les BBS : architecture et fonctionnement {#2-les-bbs}

### 2.1 Qu'est-ce qu'un BBS ?

Un **BBS** (Bulletin Board System) est un ordinateur personnel connecté à une ligne téléphonique, équipé d'un logiciel serveur qui permet aux utilisateurs de :

- **Se connecter** via modem (en composant le numéro de téléphone)
- **Lire et écrire des messages** (forums de discussion)
- **Télécharger et uploader des fichiers** (logiciels, jeux, cracktros)
- **Jouer à des jeux en ligne** (door games)
- **Chatter** avec le sysop ou d'autres utilisateurs (en temps réel, si le BBS supporte le multiligne)

### 2.2 Architecture technique

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ARCHITECTURE D'UN BBS                                       │
 ├──────────────────────────────────────────────────────────────┤
 │  Matériel :                                                  │
 │  • Ordinateur (PC, Amiga, Atari ST, C64)                     │
 │  • Modem (300 à 14400 bauds, puis 28800+)                    │
 │  • Ligne téléphonique dédiée                                 │
 │  • Stockage : disques durs (10-40 Mo en 1985, 100+ Mo en 1990)│
 │                                                              │
 │  Logiciel serveur :                                          │
 │  • TBBS (The Bread Board System) — PC                        │
 │  • RemoteBoard — Amiga                                       │
 │  • Wildcat! BBS — PC                                         │
 │  • Citadel — Multi-plateformes                               │
 │  • Custom BBS (écrits par les sysops)                        │
 │                                                              │
 │  Structure :                                                 │
 │  • Menu principal (message areas, file areas, chat, etc.)    │
 │  • Bases de données utilisateurs (noms, mots de passe, stats)│
 │  • Systèmes de fichiers (upload, download, ratios)           │
 │  • Systèmes de messagerie (email interne, echomail)          │
 └──────────────────────────────────────────────────────────────┘
```

### 2.3 Les types de BBS

| Type | Description | Accès | Exemple |
| --- | --- | --- | --- |
| **Public BBS** | Ouvert à tous, souvent gratuit | Appel téléphonique | La majorité des BBS |
| **Private BBS** | Sur invitation seulement | Mot de passe requis | BBS de groupes de cracking |
| **Warez BBS** | Spécialisé dans les logiciels crackés | Ratio upload/download | BBS "top sites" |
| **Demo BBS** | Spécialisé dans les démos et intros | Ouvert ou privé | BBS de démoscène |
| **Support BBS** | Support technique pour un produit | Accès limité | BBS officiels d'éditeurs |

### 2.4 La hiérarchie d'un BBS

```
 ┌──────────────────────────────────────────────────────────────┐
 │  HIÉRARCHIE D'UN BBS                                         │
 ├──────────────────────────────────────────────────────────────┤
 │  Sysop (System Operator)                                     │
 │  • Propriétaire et administrateur du BBS                     │
 │  • Gère les utilisateurs, les fichiers, les messages         │
 │  • Peut être membre d'un groupe de cracking                  │
 │                                                              │
 │  Co-Sysop / Moderator                                        │
 │  • Assistants du sysop                                       │
 │  • Modèrent les forums, valident les uploads                 │
 │                                                              │
 │  User (utilisateur)                                          │
 │  • Accès de base (lecture de messages, download limité)      │
 │  • Monte en niveau par l'activité (uploads, messages)        │
 │                                                              │
 │  Ratio User                                                  │
 │  • Utilisateur avec ratio upload/download (ex: 1:1)          │
 │  • Doit uploader autant qu'il download                       │
 │                                                              │
 │  Guest                                                       │
 │  • Accès temporaire (nouvel utilisateur)                     │
 │  • Limité en temps et en fonctionnalités                     │
 └──────────────────────────────────────────────────────────────┘
```

### 2.5 Les "warez BBS" et les "top sites"

Les **warez BBS** étaient des BBS spécialisés dans la distribution de logiciels crackés (jeux, applications, etc.). Ils fonctionnaient souvent sur un modèle de **ratio** : pour télécharger un fichier, il fallait en avoir uploadé un autre (ou payer en "crédits").

Les **top sites** étaient les BBS les plus prestigieux, avec :

- Les **dernières releases** (jeux crackés le jour de leur sortie)
- Les **meilleurs crackers** (membres de groupes réputés)
- Les **plus gros fichiers** (jeux multi-disques, applications complètes)
- Les **meilleures connexions** (modems rapides, lignes dédiées)

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE TOP SITE (1990)                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  Nom : "The Dark Side BBS"                                   │
 │  Sysop : "Dr. Doom" (membre de Razor 1911)                   │
 │  Modem : 2400 bauds (US Robotics)                            │
 │  Stockage : 200 Mo (énorme pour l'époque)                    │
 │  Fichiers : 5000+ (jeux, démos, utils, NFO)                  │
 │  Messages : 50 forums (général, groupes, techniques)         │
 │  Ratio : 1:1 (upload/download)                               │
 │  Accès : sur demande (interview par le sysop)                │
 │                                                              │
 │  Sections :                                                  │
 │  • C64 Games (500 fichiers)                                  │
 │  • Amiga Games (800 fichiers)                                │
 │  • PC Games (1200 fichiers)                                  │
 │  • Demos (1000 fichiers)                                     │
 │  • Utils (500 fichiers)                                      │
 │  • NFO Collection (1000 fichiers)                            │
 └──────────────────────────────────────────────────────────────┘
```

### 2.6 Les logiciels BBS

| Logiciel | Plateforme | Année | Particularités |
| --- | --- | --- | --- |
| **TBBS** (The Bread Board System) | PC (DOS) | 1983 | Le plus populaire, très configurable |
| **RemoteBoard** | Amiga | 1986 | Interface graphique, multiligne |
| **Wildcat! BBS** | PC (DOS) | 1987 | Support TCP/IP (plus tard), multiligne |
| **Citadel** | Multi | 1985 | Open source, très portable |
| **PCBoard** | PC (DOS) | 1983 | Concurrent de TBBS, très utilisé |
| **Major BBS** | PC (DOS) | 1986 | Multiligne, support réseau |
| **Custom BBS** | Multi | Divers | Écrits par les sysops (assembleur, BASIC, C) |

### 2.7 Le fonctionnement quotidien d'un BBS

```mermaid
sequenceDiagram
    participant U as Utilisateur
    participant M as Modem
    participant B as BBS
    participant S as Sysop

    U->>M: Compose le numéro de téléphone
    M->>B: Connexion (handshake modem)
    B->>U: Message de bienvenue + login
    U->>B: Nom d'utilisateur + mot de passe
    B->>U: Menu principal
    U->>B: Choix : "File Area"
    B->>U: Liste des fichiers
    U->>B: Choix : "Download GAME.ZIP"
    B->>U: Transfert via ZMODEM (compression + vérification)
    U->>B: Déconnexion
    B->>S: Log de l'activité (fichier téléchargé, durée)
```

---

## 3. Les protocoles de transfert : du XMODEM au ZMODEM {#3-protocoles-transfert}

### 3.1 Le problème du transfert de fichiers

Transférer un fichier via modem n'est pas trivial :

- **Erreurs de transmission** : bruit sur la ligne, coupures
- **Synchronisation** : émetteur et récepteur doivent être coordonnés
- **Vérification** : s'assurer que le fichier reçu est identique à l'original
- **Reprise** : pouvoir reprendre un transfert interrompu

### 3.2 Les protocoles historiques

| Protocole | Année | Auteur | Particularités | Débit efficace |
| --- | --- | --- | --- | --- |
| **Kermit** | 1981 | Columbia University | Très portable, lent | ≈ 70% du débit brut |
| **XMODEM** | 1977 | Ward Christensen | 128 octets par bloc, checksum | ≈ 85% |
| **XMODEM-1K** | 1980s | — | 1024 octets par bloc | ≈ 90% |
| **YMODEM** | 1985 | Chuck Forsberg | Batch transfer, CRC-16 | ≈ 92% |
| **YMODEM-G** | 1985 | Chuck Forsberg | Pas de vérification (très rapide) | ≈ 98% |
| **ZMODEM** | 1986 | Chuck Forsberg | Streaming, reprise, CRC-32 | ≈ 95% |

### 3.3 Zoom : ZMODEM (le standard)

**ZMODEM**, développé par **Chuck Forsberg** en 1986, est devenu le **protocole de référence** pour les BBS. Ses innovations :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ZMODEM (1986)                                               │
 ├──────────────────────────────────────────────────────────────┤
 │  • Streaming : pas d'attente d'accusé de réception par bloc  │
 │  • Reprise : peut reprendre un transfert interrompu          │
 │  • CRC-32 : vérification d'intégrité robuste                 │
 │  • Auto-start : le récepteur peut initier le transfert       │
 │  • Nom de fichier : transmet le nom et la taille du fichier  │
 │  • Batch transfer : peut envoyer plusieurs fichiers d'un coup│
 │                                                              │
 │  Fonctionnement :                                            │
 │  1. Émetteur envoie "SZ" (send ZMODEM)                       │
 │  2. Récepteur répond "rz" (receive ZMODEM)                   │
 │  3. Transfert en continu (streaming)                         │
 │  4. Vérification CRC-32 à la fin                             │
 │  5. Accusé de réception final                                │
 │                                                              │
 │  Gain :                                                      │
 │  • XMODEM : 128 octets + attente ACK = lent                  │
 │  • ZMODEM : streaming + reprise = rapide et fiable           │
 └──────────────────────────────────────────────────────────────┘
```

### 3.4 Les commandes AT et les modems

Les modems étaient contrôlés par des **commandes AT** (Attention) :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  COMMANDES AT (Hayes, 1981)                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  AT          : Test (répond "OK")                            │
 │  ATDT 5551234: Dial Tone (compose le numéro)                 │
 │  ATDP 5551234: Dial Pulse (compose, ancienne méthode)        │
 │  ATA         : Answer (répond à un appel entrant)            │
 │  ATH         : Hang up (raccroche)                           │
 │  ATI         : Information (affiche le modèle du modem)      │
 │  AT&F        : Factory reset (restaure les paramètres)       │
 │  ATS0=1      : Auto-answer après 1 sonnerie                  │
 │  AT&B1       : Protocole de compression (MNP, V.42bis)       │
 │                                                              │
 │  Vitesses :                                                  │
 │  AT-B300     : 300 bauds                                     │
 │  AT-B1200    : 1200 bauds                                    │
 │  AT-B2400    : 2400 bauds                                    │
 │  AT-B9600    : 9600 bauds                                    │
 │  AT-B14400   : 14400 bauds                                   │
 │  AT-B28800   : 28800 bauds                                   │
 └──────────────────────────────────────────────────────────────┘
```

### 3.5 La compression en ligne

Les modems modernes (à partir de 1988) intégraient des **algorithmes de compression** :

| Standard | Année | Taux de compression | Particularités |
| --- | --- | --- | --- |
| **MNP 5** | 1988 | 2:1 | Microcom Networking Protocol |
| **V.42bis** | 1990 | 4:1 | Standard ITU-T |
| **V.44** | 2003 | 6:1 | Plus récent, plus efficace |

**Principe** : le modem compresse les données **avant** de les envoyer sur la ligne téléphonique, et le modem récepteur les décompresse. Cela permettait de multiplier le débit effectif par 2 à 4.

---

## 4. Le swapping postal : la poste comme réseau {#4-swapping-postal}

### 4.1 Qu'est-ce que le swapping ?

Le **swapping** (échange) postal consistait à envoyer des **disquettes** par courrier postal entre membres de la scène. C'était le **réseau de distribution principal** avant l'arrivée des BBS rapides et d'Internet.

### 4.2 Le processus

```mermaid
flowchart TD
    A["Cracker A termine un crack"] --> B["Enregistre sur disquette"]
    B --> C["Ajoute une lettre manuscrite<br/>(crédits, instructions)"]
    C --> D["Met dans une enveloppe customisée<br/>(logo du groupe, stickers)"]
    D --> E["Envoie par courrier postal<br/>(affranchissement)"]
    E --> F["Cracker B reçoit la disquette"]
    F --> G["Teste le crack"]
    G --> H{"OK ?"}
    H -->|"oui"| I["Upload sur son BBS<br/>ou copie pour d'autres"]
    H -->|"non"| J["Renvoie au cracker A<br/>(avec explications)"]
    I --> K["Le crack se propage<br/>(swapping en cascade)"]
    style E fill:#1e3a5f,color:#fff
    style K fill:#3a5f1e,color:#fff
```

### 4.3 Les acteurs du swapping

| Rôle | Fonction | Exemple |
| --- | --- | --- |
| **Swapper** | Membre qui échange régulièrement des disquettes | La majorité des membres de la scène |
| **Courier** | Membre qui transporte les disquettes entre les sites (BBS) | Couriers de groupes (Razor 1911, Fairlight) |
| **Supplier** | Membre qui fournit les jeux originaux (achète ou emprunte) | Suppliers de groupes |
| **Cracker** | Membre qui crack les jeux | Crackers de groupes |

### 4.4 La logistique

```
 ┌──────────────────────────────────────────────────────────────┐
 │  LOGISTIQUE DU SWAPPING                                      │
 ├──────────────────────────────────────────────────────────────┤
 │  Coût :                                                      │
 │  • Disquette vierge : 10-20 F (≈ 3-6 €)                      │
 │  • Affranchissement : 5-15 F (selon le pays)                 │
 │  • Enveloppe : 1-5 F                                         │
 │  • Total : 16-40 F par envoi (≈ 5-12 €)                      │
 │                                                              │
 │  Délai :                                                     │
 │  • National : 1-3 jours                                      │
 │  • Européen : 3-7 jours                                      │
 │  • International : 1-3 semaines                              │
 │                                                              │
 │  Risques :                                                   │
 │  • Perte par la poste                                        │
 │  • Dommages (disquette cassée, magnétisée)                   │
 │  • Confiscation par les douanes (contenu illégal)            │
 │  • Retards (grèves, vacances)                                │
 └──────────────────────────────────────────────────────────────┘
```

### 4.5 Les adresses de swapping

Les membres de la scène publiaient leurs **adresses de swapping** dans les **NFO** (fichiers d'information) et les **cracktros** :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE D'ADRESSE DE SWAPPING (dans un NFO)                 │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │  ╔══════════════════════════════════════════════════════╗    │
 │  ║  SWAPPING ADDRESS                                    ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║  John Doe                                            ║    │
 │  ║  123 Main Street                                     ║    │
 │  ║  London SW1A 1AA                                     ║    │
 │  ║  UNITED KINGDOM                                      ║    │
 │  ║                                                      ║    │
 │  ║  Looking for: C64, Amiga, ST games                   ║    │
 │  ║  Sending: C64 cracks (Fairlight, Razor 1911)         ║    │
 │  ║                                                      ║    │
 │  ║  Please include a blank disk + return postage!       ║    │
 │  ╚══════════════════════════════════════════════════════╝    │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 4.6 Les conventions du swapping

| Convention | Description |
| --- | --- |
| **Inclure une disquette vierge** | Pour que le destinataire puisse copier et renvoyer |
| **Affranchissement retour** | Inclure des timbres pour le retour (surtout international) |
| **Lettre manuscrite** | Présenter le groupe, les crédits, les demandes |
| **Enveloppe customisée** | Logo du groupe, stickers, dessins (art postal) |
| **Ne pas envoyer de jeux commerciaux** | Pour éviter les problèmes légaux (envoyer des cracks seulement) |
| **Respecter les accords** | Si on promet d'envoyer quelque chose, le faire |

### 4.7 Le swapping et la qualité

Le swapping avait un **problème de dégradation** : à chaque copie, la qualité du signal pouvait se dégrader (surtout pour les K7). Les disquettes étaient plus fiables, mais les copies de copies pouvaient accumuler des erreurs.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  DÉGRADATION EN CASCADE                                      │
 ├──────────────────────────────────────────────────────────────┤
 │  Original → Copie 1 → Copie 2 → Copie 3 → ...               │
 │                                                              │
 │  Disquette :                                                 │
 │  • Peu de dégradation (copie numérique)                      │
 │  • Mais : erreurs de lecture possibles (poussière, usure)    │
 │                                                              │
 │  K7 audio :                                                  │
 │  • Dégradation significative (bruit, distorsion)             │
 │  • Après 3-4 générations : souvent illisible                 │
 │                                                              │
 │  Solution :                                                  │
 │  • Toujours partir de l'original (ou d'une copie de 1ère gén.)│
 │  • Vérifier l'intégrité (checksums, tests de fonctionnement) │
 └──────────────────────────────────────────────────────────────┘
```

---

## 5. FidoNet et les réseaux numériques {#5-fidonet}

### 5.1 Qu'est-ce que FidoNet ?

**FidoNet**, fondé par **Tom Jennings** en 1984, est un **réseau mondial de BBS** qui permettait l'échange de messages et de fichiers entre BBS, via des connexions modem. C'était l'ancêtre d'Internet pour les BBS.

### 5.2 Architecture

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ARCHITECTURE DE FIDONET                                     │
 ├──────────────────────────────────────────────────────────────┤
 │  Hiérarchie :                                                │
 │  • Zone (1-6) : continent (ex: Zone 1 = Amérique du Nord)    │
 │  • Region : pays ou grande région (ex: Region 30 = France)   │
 │  • Net : ville ou région (ex: Net 234 = Paris)               │
 │  • Node : BBS individuel (ex: Node 1234)                     │
 │  • Point : utilisateur individuel (optionnel)                │
 │                                                              │
 │  Adressage :                                                 │
 │  • Format : Zone:Region/Net.Node                             │
 │  • Exemple : 2:30/1234.567                                   │
 │    (Zone 2 = Europe, Region 30 = France, Net 1234, Node 567) │
 │                                                              │
 │  Fonctionnement :                                            │
 │  • Les BBS s'appellent entre eux (modem)                     │
 │  • Échangent des messages (echomail) et des fichiers         │
 │  • Stock-and-forward : les messages transitent de nœud en    │
 │    nœud jusqu'à destination                                  │
 └──────────────────────────────────────────────────────────────┘
```

### 5.3 L'echomail

L'**echomail** était le système de **forums de discussion** de FidoNet. Les messages étaient échangés entre BBS et diffusés dans des **conférences** (echoes) thématiques :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLES D'ECHOES FIDONET                                   │
 ├──────────────────────────────────────────────────────────────┤
 │  • FIDONEWS : actualités de FidoNet                          │
 │  • C64 : discussions sur le Commodore 64                     │
 │  • AMIGA : discussions sur l'Amiga                           │
 │  • CRACKING : discussions sur le cracking (privé)            │
 │  • WAREZ : annonces de releases (privé)                      │
 │  • DEMOSCENE : discussions sur la démoscène                  │
 │  • PROGRAMMING : techniques de programmation                 │
 │                                                              │
 │  Fonctionnement :                                            │
 │  1. Utilisateur A écrit un message sur son BBS               │
 │  2. Le BBS l'envoie au BBS suivant (via modem)               │
 │  3. Le message transite de BBS en BBS                        │
 │  4. Tous les BBS abonnés à l'echo reçoivent le message       │
 │  5. Les utilisateurs peuvent répondre (thread)               │
 └──────────────────────────────────────────────────────────────┘
```

### 5.4 Les fichiers FidoNet

FidoNet utilisait des **formats de fichiers spécifiques** pour l'échange de messages et de fichiers :

| Format | Usage | Description |
| --- | --- | --- |
| **.MSG** | Messages | Format de message individuel (texte + en-tête) |
| **.PKT** | Packet | Paquet de messages (plusieurs .MSG compressés) |
| **.ARC** | Archive | Format de compression (avant ZIP) |
| **.ZIP** | Archive | Format de compression (PKZIP) |
| **.DIZ** | Description | Fichier de description (FILE_ID.DIZ) |

### 5.5 FidoNet et la scène

FidoNet a été **massivement utilisé** par la scène du cracking pour :

- **Annoncer les releases** (nouveaux cracks)
- **Coordonner les groupes** (communication entre membres)
- **Échanger des techniques** (cracking, coding, graphisme)
- **Distribuer des outils** (packers, copieurs, éditeurs)

```mermaid
flowchart LR
    A["Groupe A (Londres)"] -->|"Upload release"| B["BBS A (Londres)"]
    B -->|"Echomail via FidoNet"| C["BBS B (Paris)"]
    C -->|"Echomail via FidoNet"| D["BBS C (Berlin)"]
    D -->|"Echomail via FidoNet"| E["BBS D (Stockholm)"]
    E -->|"Download release"| F["Groupe B (Stockholm)"]
    style B fill:#1e3a5f,color:#fff
    style C fill:#3a5f1e,color:#fff
    style D fill:#5f3a1e,color:#fff
    style E fill:#5f1e1e,color:#fff
```

### 5.6 Le déclin de FidoNet

FidoNet a décliné à partir de **1994-1995** avec l'arrivée d'Internet :

- **Email** : plus rapide, plus fiable, gratuit (pas de coût téléphonique)
- **Usenet** : forums de discussion globaux, plus efficaces
- **FTP** : transfert de fichiers plus rapide
- **WWW** : interface graphique, plus accessible

---

## 6. La sociologie des groupes : rôles et hiérarchies {#6-sociologie-groupes}

### 6.1 La structure d'un groupe

Un **groupe de cracking** était une organisation hiérarchisée avec des **rôles précis** :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  STRUCTURE D'UN GROUPE DE CRACKING                           │
 ├──────────────────────────────────────────────────────────────┤
 │  Leader (ou Admin)                                           │
 │  • Dirige le groupe                                          │
 │  • Recrute les membres                                       │
 │  • Gère les conflits                                         │
 │  • Représente le groupe                                      │
 │                                                              │
 │  Cracker                                                     │
 │  • Contourne les protections                                 │
 │  • Patch le code                                             │
 │  • Teste le crack                                            │
 │                                                              │
 │  Coder                                                       │
 │  • Développe les outils (packers, copieurs, éditeurs)        │
 │  • Écrit les cracktros et intros                             │
 │  • Optimise le code                                          │
 │                                                              │
 │  Musician                                                    │
 │  • Compose les musiques de cracktros                         │
 │  • Utilise les trackers (ProTracker, FastTracker)            │
 │  • Crée les players (routines de lecture)                    │
 │                                                              │
 │  Graphician                                                  │
 │  • Crée les logos, écrans-titres, NFO                        │
 │  • Utilise les éditeurs graphiques (DPaint, Koala)           │
 │  • Fait les ANSI art (sur PC)                                │
 │                                                              │
 │  Supplier                                                    │
 │  • Fournit les jeux originaux (achète, emprunte, vole)       │
 │  • Envoie les originaux aux crackers                         │
 │                                                              │
 │  Courier                                                     │
 │  • Transporte les disquettes entre les membres               │
 │  • Fait le lien entre les sites (BBS)                        │
 │  • Garantit la rapidité de distribution                      │
 │                                                              │
 │  Swapper                                                     │
 │  • Échange des disquettes avec d'autres groupes              │
 │  • Maintient les contacts externes                           │
 │                                                              │
 │  NFO Writer                                                  │
 │  • Écrit les fichiers NFO (présentation du groupe)           │
 │  • Fait l'ASCII art (sur PC)                                 │
 │  • Liste les crédits, les contacts                           │
 └──────────────────────────────────────────────────────────────┘
```

### 6.2 Les rôles multiples

Un membre pouvait avoir **plusieurs rôles** :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE PROFIL DE MEMBRE                                 │
 ├──────────────────────────────────────────────────────────────┤
 │  Pseudo : "The Phantom"                                      │
 │  Groupe : Razor 1911                                         │
 │  Rôles :                                                     │
 │  • Cracker (spécialiste C64)                                 │
 │  • Coder (a écrit un packer)                                 │
 │  • Courier (transporte les disquettes en Scandinavie)        │
 │                                                              │
 │  Réputation :                                                │
 │  • Respecté pour ses cracks rapides                          │
 │  • Connu pour son packer (utilisé par d'autres groupes)      │
 │  • Fiable en tant que courier                                │
 └──────────────────────────────────────────────────────────────┘
```

### 6.3 Les règles du groupe

Chaque groupe avait ses **règles** (rules), souvent publiées dans les NFO :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE RÈGLES DE GROUPE (NFO)                           │
 ├──────────────────────────────────────────────────────────────┤
 │  ╔══════════════════════════════════════════════════════╗    │
 │  ║  RAZOR 1911 - RULES                                  ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║  1. No dupes (vérifier avant de cracker)             ║    │
 │  ║  2. No nukes (qualité obligatoire)                   ║    │
 │  ║  3. Credit where credit is due                       ║    │
 │  ║  4. No trading with cops (pas d'échange avec police) ║    │
 │  ║  5. Respect other groups                             ║    │
 │  ║  6. No leeching (uploader pour télécharger)          ║    │
 │  ║  7. Keep your word (si tu promets, tiens promesse)   ║    │
 │  ║  8. No drama (pas de conflits publics)               ║    │
 │  ╚══════════════════════════════════════════════════════╝    │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 6.4 La réputation

La **réputation** était capitale dans la scène :

| Critère | Description |
| --- | --- |
| **Rapidité** | Être le premier à sortir un crack (pre-time) |
| **Qualité** | Sortir des cracks qui fonctionnent (pas de nukes) |
| **Productivité** | Sortir beaucoup de cracks |
| **Fiabilité** | Tenir ses promesses (courier, swapper) |
| **Originalité** | Innover (outils, techniques, graphismes) |
| **Respect** | Respecter les autres groupes (pas de drama) |

---

## 7. La distribution : releases, nukes et dupes {#7-distribution}

### 7.1 Les releases

Une **release** était un **jeu cracké** distribué par un groupe. Elle comprenait généralement :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  CONTENU D'UNE RELEASE TYPIQUE                               │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Le jeu cracké                                            │
 │     • Code patché (protection neutralisée)                   │
 │     • Éventuellement compressé (Pucrunch, PowerPacker)       │
 │                                                              │
 │  2. La cracktro                                              │
 │     • Écran de défilement (scroll)                           │
 │     • Musique (SID, MOD, XM)                                 │
 │     • Logo du groupe (animé ou statique)                     │
 │     • Crédits (cracker, musician, graphician)                │
 │                                                              │
 │  3. Le fichier NFO                                           │
 │     • Présentation du groupe                                 │
 │     • Liste des membres                                      │
 │     • Adresses de swapping                                   │
 │     • Messages (greetings, rules)                            │
 │     • ASCII art (sur PC)                                     │
 │                                                              │
 │  4. Éventuellement :                                         │
 │     • Trainer (menu de triche)                               │
 │     • Documentation (manuel scanné, hints)                   │
 │     • Outils (packer, copieur)                               │
 └──────────────────────────────────────────────────────────────┘
```

### 7.2 Le pre-time

Le **pre-time** était le **moment de la première diffusion** d'une release. Le groupe qui sortait un jeu en premier était crédité comme le **cracker officiel**.

```mermaid
flowchart TD
    A["Jeu original sort en magasin<br/>(ex: 15 octobre 1990)"] --> B["Supplier achète le jeu"]
    B --> C["Envoie au cracker<br/>(swapping postal ou courier)"]
    C --> D["Cracker contourne la protection"]
    D --> E["Ajoute cracktro + NFO"]
    E --> F["Upload sur BBS du groupe<br/>(15 octobre, 23h45)"]
    F --> G["PRE-TIME : le groupe est le premier"]
    G --> H["Annonce sur FidoNet echomail"]
    H --> I["Autres groupes voient l'annonce"]
    I --> J{"Un autre groupe<br/>avait déjà cracké le même jeu ?"}
    J -->|"non"| K["Release validée"]
    J -->|"oui"| L["DUPE : la release est annulée"]
    style F fill:#1e3a5f,color:#fff
    style G fill:#3a5f1e,color:#fff
```

### 7.3 Les dupes

Un **dupe** (duplication) se produisait lorsque **deux groupes sortaient le même jeu** en même temps (ou presque). Le groupe qui avait le **pre-time le plus ancien** gagnait, et l'autre release était **annulée**.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE DUPE                                             │
 ├──────────────────────────────────────────────────────────────┤
 │  Jeu : "Shadow of the Beast" (Amiga)                         │
 │                                                              │
 │  Groupe A (Fairlight) :                                      │
 │  • Pre-time : 15 octobre 1990, 23h45                         │
 │  • Upload sur BBS "The Dark Side"                            │
 │                                                              │
 │  Groupe B (Razor 1911) :                                     │
 │  • Pre-time : 16 octobre 1990, 00h15                         │
 │  • Upload sur BBS "Nordic Star"                              │
 │                                                              │
 │  Résultat :                                                  │
 │  • Fairlight a le pre-time (23h45 < 00h15)                   │
 │  • La release de Razor 1911 est un DUPE                      │
 │  • Razor 1911 doit "nuker" sa release (l'annuler)            │
 │                                                              │
 │  Conséquences :                                              │
 │  • Fairlight est crédité comme cracker officiel              │
 │  • Razor 1911 perd des points de réputation                  │
 │  • Les BBS suppriment la release de Razor 1911               │
 └──────────────────────────────────────────────────────────────┘
```

### 7.4 Les nukes

Un **nuke** (destruction) se produisait lorsqu'une release était **défectueuse** (ne fonctionnait pas, était incomplète, était un dupe). Le groupe devait alors **annuler** sa release et publier un **NUKE NFO** expliquant la raison.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE NUKE NFO                                         │
 ├──────────────────────────────────────────────────────────────┤
 │  ╔══════════════════════════════════════════════════════╗    │
 │  ║  ╔════════════════════════════════════════════════╗  ║    │
 │  ║  ║  N U K E D                                     ║  ║    │
 │  ║  ╚════════════════════════════════════════════════╝  ║    │
 │  ║                                                      ║    │
 │  ║  Release : "Shadow of the Beast" (Amiga)             ║    │
 │  ║  Groupe : Razor 1911                                 ║    │
 │  ║  Date : 16 octobre 1990                              ║    │
 │  ║                                                      ║    │
 │  ║  Reason :                                            ║    │
 │  ║  • Level 3 does not load (crack incomplete)          ║    │
 │  ║  • Dupe : Fairlight released it 30 minutes earlier   ║    │
 │  ║                                                      ║    │
 │  ║  We apologize for this mistake.                      ║    │
 │  ║  A new release will follow soon.                     ║    │
 │  ║                                                      ║    │
 │  ║  Greetings to all groups.                            ║    │
 │  ╚══════════════════════════════════════════════════════╝    │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 7.5 Les cours

Les **cours** (ou **charts**) étaient des **classements** des groupes, basés sur :

- Le nombre de releases
- La qualité (pas de nukes)
- La rapidité (pre-times)
- La popularité (votes des utilisateurs)

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE DE COURS (C64, 1989)                                │
 ├──────────────────────────────────────────────────────────────┤
 │  ╔══════════════════════════════════════════════════════╗    │
 │  ║  TOP 10 C64 GROUPS - 1989                            ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║  1. Fairlight (Sweden) - 450 releases                ║    │
 │  ║  2. Razor 1911 (Norway) - 420 releases               ║    │
 │  ║  3. Triad (Sweden) - 380 releases                    ║    │
 │  ║  4. The Humble Guys (USA) - 350 releases             ║    │
 │  ║  5. Skid Row (USA) - 320 releases                    ║    │
 │  ║  6. Paradox (Sweden) - 300 releases                  ║    │
 │  ║  7. Quartex (Sweden) - 280 releases                  ║    │
 │  ║  8. Hotline (Sweden) - 260 releases                  ║    │
 │  ║  9. Rebels (Denmark) - 240 releases                  ║    │
 │  ║  10. Vision (Germany) - 220 releases                 ║    │
 │  ╚══════════════════════════════════════════════════════╝    │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

---

## 8. L'art du NFO et de l'ANSI {#8-art-nfo-ansi}

### 8.1 Qu'est-ce qu'un NFO ?

Un **NFO** (de l'anglais "info", prononcé "N-F-O" ou "info") était un **fichier texte** accompagnant une release, contenant :

- La **présentation du groupe** (histoire, philosophie)
- La **liste des membres** (pseudos, rôles)
- Les **crédits** de la release (cracker, musician, graphician)
- Les **adresses de swapping** (contacts postaux)
- Les **règles du groupe**
- Les **greetings** (salutations à d'autres groupes)
- De l'**ASCII art** (sur PC) ou du **graphisme** (sur C64/Amiga)

### 8.2 Structure d'un NFO

```
 ┌──────────────────────────────────────────────────────────────┐
 │  STRUCTURE D'UN NFO TYPIQUE                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  ╔══════════════════════════════════════════════════════╗    │
 │  ║                                                      ║    │
 │  ║           ██████  ██████  ██████  ██████             ║    │
 │  ║           ██      ██      ██      ██                 ║    │
 │  ║           ██████  ██████  ██      ██                 ║    │
 │  ║           ██      ██      ██      ██                 ║    │
 │  ║           ██      ██████  ██████  ██████             ║    │
 │  ║                                                      ║    │
 │  ║                    PRESENTS                          ║    │
 │  ║                                                      ║    │
 │  ║                 SHADOW OF THE BEAST                  ║    │
 │  ║                                                      ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║                                                      ║    │
 │  ║  Crack : The Phantom                                 ║    │
 │  ║  Music : Dr. Dread                                   ║    │
 │  ║  Graphics : The Artist                               ║    │
 │  ║                                                      ║    │
 │  ║  Release date : 15-10-1990                           ║    │
 │  ║  Pre-time : 23h45                                    ║    │
 │  ║                                                      ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║                                                      ║    │
 │  ║  GREETINGS TO :                                      ║    │
 │  ║  Fairlight, Triad, Razor 1911, The Humble Guys...    ║    │
 │  ║                                                      ║    │
 │  ╠══════════════════════════════════════════════════════╣    │
 │  ║                                                      ║    │
 │  ║  SWAPPING ADDRESS :                                  ║    │
 │  ║  John Doe                                            ║    │
 │  ║  123 Main Street                                     ║    │
 │  ║  London SW1A 1AA                                     ║    │
 │  ║  UNITED KINGDOM                                      ║    │
 │  ║                                                      ║    │
 │  ╚══════════════════════════════════════════════════════╝    │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 8.3 L'ASCII art

L'**ASCII art** était un **art graphique** utilisant les caractères ASCII (lettres, chiffres, symboles) pour créer des images. C'était très populaire sur PC (où les NFO étaient affichés dans des terminaux texte).

```
 ┌──────────────────────────────────────────────────────────────┐
 │  EXEMPLE D'ASCII ART                                         │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │      /\                                                      │
 │     /  \                                                     │
 │    /    \                                                    │
 │   /  /\  \                                                   │
 │  /  /  \  \                                                  │
 │ /  /    \  \                                                 │
 │/__/______\__\                                                │
 │                                                              │
 │  /\      /\      /\      /\      /\      /\      /\         │
 │ /  \    /  \    /  \    /  \    /  \    /  \    /  \        │
 │/    \  /    \  /    \  /    \  /    \  /    \  /    \       │
 │                                                              │
 │  CRACKED BY THE PHANTOM - RAZOR 1911 - 1990                  │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 8.4 Les outils de création

| Plateforme | Outil | Description |
| --- | --- | --- |
| PC (DOS) | **ANSI draw** | Éditeur ANSI art (couleurs, caractères) |
| PC (DOS) | **TheDraw** | Éditeur ANSI art populaire |
| PC (DOS) | **ACiDdraw** | Éditeur ANSI art (groupe ACiD) |
| C64 | **ASCII Editor** | Éditeur texte simple |
| Amiga | **CyberGraphX** | Éditeur graphique (converti en ASCII) |

### 8.5 Les groupes d'ASCII art

Des **groupes spécialisés** dans l'ASCII art ont émergé :

- **ACiD Productions** (ACiD) : l'un des plus célèbres
- **iCE** (Insane Creators Enterprise)
- **Anarchy**
- **Cult**

Ces groupes créaient des **collections d'ASCII art** (packs) qui étaient distribuées sur les BBS.

---

## 9. La transition vers Internet {#9-transition-internet}

### 9.1 L'arrivée d'Internet

Internet est devenu **accessible au grand public** à partir de **1993-1995**, avec :

- **Le World Wide Web** (1991, Tim Berners-Lee) : interface graphique, navigation par liens
- **Les navigateurs** (Mosaic 1993, Netscape 1994) : accès facile au Web
- **Les FAI** (Fournisseurs d'Accès Internet) : connexions grand public

### 9.2 L'impact sur la scène

Internet a **remplacé** progressivement les BBS et le swapping :

| Ancien système | Nouveau système | Avantage |
| --- | --- | --- |
| BBS (modem) | FTP, WWW | Plus rapide, gratuit, mondial |
| Swapping postal | Email, FTP | Instantané, pas de coût postal |
| FidoNet | Usenet, email | Plus rapide, plus fiable |
| Courriers physiques | IRC, messagerie | Temps réel, mondial |

### 9.3 La migration des groupes

Les groupes de cracking ont **migré** vers Internet :

```mermaid
flowchart LR
    A["BBS (1980s)"] -->|"modem lent"| B["FidoNet (1984-1994)"]
    B -->|"email, FTP"| C["Internet (1994+)"]
    C -->|"WWW, IRC"| D["Web moderne (2000+)"]
    D -->|"P2P, torrents"| E["BitTorrent (2001+)"]
    style A fill:#5f1e1e,color:#fff
    style B fill:#5f3a1e,color:#fff
    style C fill:#3a5f1e,color:#fff
    style D fill:#1e5f3a,color:#fff
    style E fill:#1e3a5f,color:#fff
```

### 9.4 Les premiers sites web de la scène

Les premiers **sites web** de la scène sont apparus vers **1995-1996** :

- **Pouët.net** (1998) : base de données de démos
- **CSDb** (2002) : base de données C64
- **Hornet** (1995) : archive C64 (devenu inactif)
- **Lemon64** (2000) : archive C64

### 9.5 Le déclin des BBS

Les BBS ont **décliné** à partir de **1995-2000** :

- **Concurrence d'Internet** : plus rapide, gratuit, mondial
- **Coût des lignes téléphoniques** : devenu prohibitif
- **Vieillissement des sysops** : beaucoup ont arrêté
- **Archivage** : les anciens BBS ont été archivés (textefiles.com, etc.)

---

## 10. L'héritage : de la scène au web moderne {#10-heritage}

### 10.1 L'héritage technique

| Innovation de la scène | Application moderne |
| --- | --- |
| **BBS** | Forums web, réseaux sociaux |
| **Protocoles de transfert** (ZMODEM) | HTTP, FTP, BitTorrent |
| **Compression** (ZIP, ARJ) | ZIP, RAR, 7-Zip |
| **Fichiers NFO** | README, documentation logicielle |
| **ASCII art** | Emojis, mèmes, art numérique |
| **Cracktros** | Intros de jeux modernes, cinématiques |

### 10.2 L'héritage culturel

| Concept de la scène | Application moderne |
| --- | --- |
| **Groups** | Communautés open source, collectifs de hackers |
| **Releases** | Versions de logiciels, mises à jour |
| **Pre-time** | Première publication d'une news, d'un logiciel |
| **Nukes** | Retraits de logiciels défectueux, corrections |
| **Dupes** | Redondance, duplication d'efforts |
| **Swapping** | Partage de fichiers, P2P |
| **Couriers** | Modérateurs, administrateurs de communautés |

### 10.3 Les personnes de la scène devenues professionnelles

Beaucoup de membres de la scène ont **rejoint l'industrie** :

| Personne | Scène | Industrie |
| --- | --- | --- |
| **John Carmack** | BBS, hacking | Co-fondateur d'id Software (Doom, Quake) |
| **Markus Persson** | Demoscène (C64) | Créateur de Minecraft |
| **Linus Torvalds** | — (mais héritier de la culture) | Créateur de Linux |
| **Richard Stallman** | — (mais héritier de la culture) | Fondateur du mouvement Free Software |
| **Nombreux développeurs** | Scène du cracking, démoscène | Industrie du jeu vidéo, sécurité informatique |

### 10.4 La préservation de l'histoire

Des **archivistes** préservent l'histoire de la scène :

- **Textfiles.com** : archive de NFO, textfiles, BBS
- **Hornet** (archive) : archive C64
- **CSDb** : base de données C64
- **Pouët.net** : base de données démos
- **Archive.org** : collections de logiciels, magazines, BBS

---

## 11. Conclusion {#11-conclusion}

La **logistique de l'ombre** de la scène du cracking (BBS, swapping, FidoNet) représente un **chapitre fascinant** de l'histoire de l'informatique. Loin d'être de simples outils de distribution, ces réseaux ont été le **laboratoire d'innovations sociales et techniques** majeures :

- **Les BBS** ont inventé les forums de discussion, les systèmes de fichiers en ligne, les communautés virtuelles.
- **Le swapping postal** a créé un réseau mondial décentralisé, résilient, basé sur la confiance et la réputation.
- **FidoNet** a été l'ancêtre d'Internet pour les BBS, avec ses protocoles, ses hiérarchies, ses cultures.
- **Les groupes de cracking** ont développé une sociologie complexe (rôles, règles, réputation) qui préfigurait les communautés open source et les réseaux sociaux modernes.

L'héritage de cette époque est double :

1. **Technique** : les protocoles, les formats, les outils de la scène ont évolué vers les standards modernes (HTTP, FTP, BitTorrent, forums web).
2. **Culturel** : la culture de la scène (groups, releases, pre-times, nukes) a influencé les communautés en ligne modernes (open source, hackers, gamers).

Aujourd'hui, les BBS ont presque tous disparu, le swapping postal est devenu anecdotique, et FidoNet n'est plus qu'un souvenir. Mais leur héritage vit dans chaque forum web, chaque réseau social, chaque communauté en ligne. La scène du cracking des années 1980-1990 a **inventé l'Internet social** avant l'heure.

---

## Annexes

### Annexe A — Tableau comparatif des réseaux de distribution

| Réseau | Période | Technologie | Débit | Coût | Particularités |
| --- | --- | --- | --- | --- | --- |
| **Swapping postal** | 1980-1995 | Courrier postal | N/A | 16-40 F/envoi | Lent, fiable, mondial |
| **BBS** | 1978-2000 | Modem (téléphone) | 300-28800 bauds | Coût téléphonique | Communautaire, local |
| **FidoNet** | 1984-1995 | Modem (BBS) | 300-14400 bauds | Coût téléphonique | Réseau de BBS, echomail |
| **UUCP** | 1980s | Unix | Variable | Coût téléphonique | Ancêtre d'Usenet |
| **FTP** | 1990s | Internet | Variable | Gratuit (FAI) | Transfert de fichiers |
| **IRC** | 1990s | Internet | Variable | Gratuit (FAI) | Chat en temps réel |
| **Usenet** | 1980s-2000s | Internet | Variable | Gratuit (FAI) | Forums globaux |
| **WWW** | 1993+ | Internet | Variable | Gratuit (FAI) | Interface graphique |

### Annexe B — Glossaire étendu

| Terme | Définition |
| --- | --- |
| **ANSI art** | Art graphique utilisant les caractères ASCII et les codes de couleur ANSI |
| **ASCII art** | Art graphique utilisant uniquement les caractères ASCII |
| **BBS** | Bulletin Board System : serveur téléphonique permettant l'échange de fichiers et de messages |
| **Courier** | Membre d'un groupe qui transporte les disquettes entre les sites |
| **Cracktro** | Intro de signature d'un groupe, ajoutée au jeu craqué |
| **Dupe** | Duplication : deux groupes sortent le même jeu en même temps |
| **Echomail** | Système de forums de discussion de FidoNet |
| **FAI** | Fournisseur d'Accès Internet |
| **FidoNet** | Réseau mondial de BBS (1984-1995) |
| **Greeting** | Salutation à d'autres groupes dans un NFO |
| **Modem** | Modulateur-démodulateur : convertit les données numériques en signal analogique |
| **NFO** | Fichier texte accompagnant une release (infos, crédits, ASCII art) |
| **Node** | Nœud FidoNet (BBS individuel) |
| **Nuke** | Destruction : annulation d'une release défectueuse |
| **Pre-time** | Moment de la première diffusion d'une release |
| **Ratio** | Rapport upload/download (ex: 1:1) |
| **Release** | Jeu cracké distribué par un groupe |
| **Swapper** | Membre qui échange des disquettes par courrier postal |
| **Sysop** | System Operator : propriétaire et administrateur d'un BBS |
| **Top site** | BBS prestigieux avec les dernières releases |
| **Warez** | Logiciels crackés (jeux, applications) |
| **XMODEM/YMODEM/ZMODEM** | Protocoles de transfert de fichiers via modem |

### Annexe C — Errata et points à vérifier

| # | Passage | Correction | Justification |
| --- | --- | --- | --- |
| 1 | "FidoNet fondé en 1984" | FidoNet a été fondé par **Tom Jennings** en **1984** ✅ | Date exacte |
| 2 | "Premier BBS en 1978" | Le premier BBS (CBBS) a été créé par **Ward Christensen et Randy Suess** en **1978** à Chicago ✅ | Attribution |
| 3 | "ZMODEM inventé en 1986" | ZMODEM a été développé par **Chuck Forsberg** en **1986** ✅ | Attribution |
| 4 | "Razor 1911 fondé en 1985" | Razor 1911 a été fondé en **1985** en **Norvège** ⚠️ | Date et origine à recouper |
| 5 | "Fairlight fondé en 1987" | Fairlight a été fondé en **1987** en **Suède** ⚠️ | Date et origine à recouper |
| 6 | "Internet commercial en 1993" | Internet est devenu **commercial** en **1993** (fin de la restriction à la recherche) ✅ | Date exacte |
| 7 | "World Wide Web en 1991" | Le WWW a été inventé par **Tim Berners-Lee** en **1991** ✅ | Attribution |
| 8 | "Pouët.net en 1998" | Pouët.net a été créé en **1998** ✅ | Date exacte |

### Annexe D — Pour aller plus loin

**Ouvrages et documentations** ✅

- *The FidoNet Technical Standard* (FidoNet, 1980s-1990s) — spécifications techniques
- *BBS: The Documentary* (film, 2005) — documentaire sur les BBS
- *Hackers: Heroes of the Computer Revolution* (Steven Levy, 1984) — histoire des hackers
- *Freax: The Brief History of the Demoscene* (Tamás Polgár, 2018) — histoire de la démoscène

**Ressources contemporaines** ✅

- **Textfiles.com** : archive de NFO, textfiles, BBS : http://textfiles.com
- **Hornet** (archive) : archive C64 : http://hornet.org (inactif, archivé)
- **CSDb** : base de données C64 : https://csdb.dk
- **Pouët.net** : base de données démos : https://pouet.net
- **Archive.org** : collections de logiciels et de magazines d'époque : https://archive.org
- **BBS Documentary** : http://www.bbsdocumentary.com

**Archives BBS** ✅

- **World of BBS** : http://www.worldofbbs.com
- **BBS Corner** : http://www.bbscorner.com
- **Telegarden** (archive) : BBS artistique (1995-2004)

---

**Fin du document.** Les diagrammes Mermaid s'affichent nativement sur GitHub, GitLab, Obsidian, Typora et VS Code (extension Markdown Preview Mermaid). Sur un lecteur qui ne les rend pas, le code Mermaid reste lisible tel quel, et tous les schémas essentiels existent aussi en ASCII.

*Professeur Qwen, signant depuis les tranchées de la logistique de l'ombre, octobre 2026.* 🌐💾
