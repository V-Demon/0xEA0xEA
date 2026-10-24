# 📼 Les Protections sur K7 et les Loaders — Du "PRESS PLAY ON TAPE" à la préservation numérique
## Rapport technique approfondi — Édition illustrée

| | |
| --- | --- |
| Périmètre | Commodore 64/128, ZX Spectrum, Amstrad CPC, ZX81, Oric, Thomson, MSX, Atari 8 bits, BBC Micro, et périphérie Amiga/ST (cassettes audio) |
| Axe | Le support cassette comme vecteur de logiciels : loaders éditeurs, protections spécifiques, outils de copie et de dump, culture du chargement, préservation moderne |
| Position dans la série | **Troisième volet** après *Le Matériel de Cracking* (disquettes) et *L'Art de la Protection* (disquettes) |
| Illustrations | Diagrammes [Mermaid](https://mermaid.js.org) et schémas ASCII |

### Légende des niveaux de confiance

| Marque | Signification |
| --- | --- |
| ✅ | Fait solidement établi (documentation officielle, formats de préservation) |
| ⚠️ | Information de seconde main ou contradictoire selon les sources |
| 🔧 | Correction ou précision apportée par rapport à la littérature courante |

---

## Sommaire

- [0. Vue d'ensemble : un support linéaire, une guerre de timings](#0-vue-densemble)
- [1. Introduction : pourquoi la cassette a régné](#1-introduction)
- [2. Fondamentaux : la cassette audio comme support de données](#2-fondamentaux)
- [3. Les loaders « officiels » (ROM) : la base commune](#3-loaders-officiels)
- [4. Les loaders propriétaires des éditeurs](#4-loaders-proprietaires)
- [5. Les protections spécifiques K7](#5-protections-specifiques)
- [6. Les outils des crackers : copier, dumper, accélérer](#6-outils-crackers)
- [7. Études de cas par plateforme](#7-etudes-de-cas)
- [8. La culture du chargement : bruits, écrans, temps](#8-culture-chargement)
- [9. La préservation moderne : du TAP au TZX](#9-preservation-moderne)
- [10. Conclusion](#10-conclusion)
- [Annexes](#annexes)

---

## 0. Vue d'ensemble : un support linéaire, une guerre de timings {#0-vue-densemble}

### 0.1 Frise chronologique

```mermaid
timeline
    title Le support cassette et ses loaders (1977-2020)
    1977 : Commodore PET (datasette), Apple II (pas de K7 native)
    1979 : Atari 400/800 et leur cassette audio
    1980 : ZX81 (loader ROM 300/1500 bauds)
    1982 : Commodore 64 (datasette, loader ROM 300 bauds)
         : ZX Spectrum 48K (loader ROM 1200/2400 bauds)
    1983 : Amstrad CPC 464 (cassette intégrée, loader ROM)
         : Oric-1 / Oric Atmos (loader ROM 300/2400 bauds)
    1984 : Thomson TO7/TO7-70 (loader ROM)
         : MSX (loader ROM 1200 bauds)
         : BBC Micro (loader ROM 300/1200 bauds)
    1985 : Speedlock 1 (Spectrum) — premier loader propriétaire massif
         : TurboTape (C64) — loaders éditeurs C64
    1986 : Alkatraz (Spectrum, CPC)
         : Speedlock 2, 3 (anti-debug, timings)
    1987 : Speedlock 4, 5 (checksums, auto-modif)
         : Paul Owens' Protection System (POPS) sur Spectrum
    1988 : Speedlock 6, 7 (obfuscation, timings avancés)
         : Fireload, Bleepload (Spectrum)
    1989 : Fin de l'âge d'or de la K7, montée de la disquette
    1992 : Format TAP (première préservation numérique C64)
    1995 : Format TZX (ZX Spectrum, préservation multi-plateformes)
    2000s : Format CDT (CPC), PZX (Spectrum, moderne)
    2010s : Dumpers K7 modernes (MakeTZX, KryoFlux audio)
```

### 0.2 Cartographie des familles de loaders

```
                          ┌─────────────────────────────────────────┐
                          │   LOADERS ET PROTECTIONS K7 (1980-1995) │
                          └──────────────┬──────────────────────────┘
                                         │
         ┌───────────────┬───────────────┼───────────────┬───────────────┐
         ▼               ▼               ▼               ▼               ▼
   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
   │ OFFICIEL │   │ ÉDITEUR  │   │ PROTEC-  │   │ CRACKER  │   │ PRÉSER-  │
   │ (ROM)    │   │ (PROPR.) │   │ TION     │   │ (COPIE)  │   │ VATION   │
   └──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
         │               │               │               │               │
         ▼               ▼               ▼               ▼               ▼
   C64 datasette   TurboTape       Speedlock       Copie K7→K7     TAP, TZX
   Spectrum ROM    SeaSucker       Alkatraz        Dump numérique  CDT, PZX
   CPC ROM         Fireload        POPS            Fast loaders    MakeTZX
   Atari SIO       Bleepload       Timings         Tape trading    Émulateurs
```

### 0.3 La boucle du duel sur K7

```mermaid
flowchart LR
    A["Éditeur : loader ROM<br/>(lent, standard)"] -->|"copie K7→K7 triviale"| B["Copie facile"]
    B --> C["Éditeur : loader propriétaire<br/>(format maison, rapide)"]
    C -->|"le loader ROM ne sait plus lire"| D["Copie K7→K7 standard échoue"]
    D --> E["Scène : dump numérique<br/>ou copie avec le bon loader"]
    E -->|"conversion TAP/TZX<br/>ou copie avec loader éditeur"| F["Protection contournée"]
    F --> G["Éditeur : timings, checksums,<br/>silences, auto-modif"]
    G --> E
    style E fill:#1e3a5f,color:#fff
    style C fill:#5f1e1e,color:#fff
    style G fill:#5f3a1e,color:#fff
```

---

## 1. Introduction : pourquoi la cassette a régné {#1-introduction}

Avant la disquette (chère, ≈ 1500 F en 1985), avant le CD-ROM (années 1990), la **cassette audio compact** était le support universel de distribution des logiciels. Elle coûtait 20 à 50 F, tenait 30 à 90 minutes, et se lisait sur n'importe quel magnétophone du commerce — ou sur le datasette dédié de la machine.

### 1.1 Les avantages de la cassette

| Avantage | Détail |
| --- | --- |
| **Coût** | 10 à 50 fois moins chère qu'une disquette |
| **Universalité** | Tout magnétophone peut lire/écrire |
| **Capacité** | 30 à 90 minutes (≈ 50 à 150 Ko en loader rapide) |
| **Durabilité** | Support robuste (pas de tête de lecture fragile) |
| **Distribution** | Facile à dupliquer industriellement (pressage) |

### 1.2 Les inconvénients structurels

| Inconvénient | Conséquence |
| --- | --- |
| **Support linéaire** | Pas d'accès aléatoire : il faut dérouler la bande |
| **Vitesse variable** | La vitesse de défilement dépend du magnétophone (± 5 %) |
| **Qualité audio** | Bruit, distorsion, démagnétisation |
| **Temps de chargement** | De 30 secondes à 15 minutes pour un jeu complet |
| **Pas de protection physique** | Impossible de créer des « weak bits » ou des « long tracks » |

### 1.3 Le paradoxe de la cassette

La cassette est **le support le plus facile à copier** (il suffit d'un deuxième magnétophone) et **le plus difficile à protéger**. Les éditeurs ont donc dû innover non pas au niveau du support (comme sur disquette), mais au niveau du **format de données** et du **logiciel de chargement** (le « loader »).

C'est pourquoi l'histoire des protections K7 est avant tout une **histoire de loaders** : des programmes qui transforment un signal audio en données numériques, avec des formats propriétaires, des timings, des checksums, et parfois des pièges.

---

## 2. Fondamentaux : la cassette audio comme support de données {#2-fondamentaux}

### 2.1 Du signal audio au bit

Une cassette audio enregistre des **variations de tension** (signal analogique). Pour y stocker des données numériques, on utilise une **modulation** :

| Modulation | Principe | Utilisée par |
| --- | --- | --- |
| **FSK** (Frequency Shift Keying) | Deux fréquences distinctes pour 0 et 1 | C64 (datasette), Spectrum (ROM), CPC (ROM) |
| **Manchester** | Transition au milieu de chaque bit | Certains loaders propriétaires |
| **PWM** (Pulse Width Modulation) | Largeur d'impulsion variable | Quelques loaders exotiques |

### 2.2 Le cas du Commodore 64 : la datasette

Le C64 utilise une **datasette** (pas un magnétophone standard) qui communique avec la machine via un port série propriétaire. Le signal est une **onde carrée** dont la fréquence encode les bits :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  SIGNAL DATASETTE C64 (loader ROM)                           │
 ├──────────────────────────────────────────────────────────────┤
 │  Bit 0 : onde carrée à 1480 Hz (période ≈ 676 µs)            │
 │  Bit 1 : onde carrée à 833 Hz (période ≈ 1200 µs)            │
 │                                                              │
 │  ┌─────┐     ┌─────┐     ┌─────────┐           ┌─────────┐  │
 │  │     │     │     │     │         │           │         │  │
 │──┘     └─────┘     └─────┘         └───────────┘         └──│
 │  ← 676 µs →          ← 1200 µs →                            │
 │    (bit 0)               (bit 1)                              │
 └──────────────────────────────────────────────────────────────┘
```

**Débit** : ≈ 300 bauds (≈ 300 bits/s), soit ≈ 37 octets/s. Un jeu de 40 Ko se charge en ≈ 18 minutes.

### 2.3 Le cas du ZX Spectrum : le loader ROM

Le Spectrum utilise un **magnétophone standard** (pas de datasette dédiée). Le signal est également en FSK, mais avec des fréquences différentes :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  SIGNAL SPECTRUM ROM                                         │
 ├──────────────────────────────────────────────────────────────┤
 │  Pilote (sync) : onde carrée à 2400 Hz (période ≈ 417 µs)    │
 │  Bit 0 : onde carrée à 2400 Hz (2 cycles = 833 µs)           │
 │  Bit 1 : onde carrée à 1200 Hz (1 cycle = 833 µs)            │
 │                                                              │
 │  Débit : 1200 bauds (≈ 150 octets/s) pour les données        │
 │  Un jeu de 40 Ko se charge en ≈ 4-5 minutes                  │
 └──────────────────────────────────────────────────────────────┘
```

### 2.4 Le cas de l'Amstrad CPC

Le CPC 464 a un **magnétophone intégré** (pas de datasette externe). Le signal est similaire au Spectrum, mais avec des timings légèrement différents :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  SIGNAL CPC ROM                                              │
 ├──────────────────────────────────────────────────────────────┤
 │  Pilote : onde carrée à 2000 Hz                              │
 │  Bit 0 : 2 cycles à 2000 Hz                                  │
 │  Bit 1 : 1 cycle à 1000 Hz                                   │
 │                                                              │
 │  Débit : ≈ 1000 bauds (≈ 125 octets/s)                       │
 └──────────────────────────────────────────────────────────────┘
```

### 2.5 Pourquoi les loaders propriétaires ?

Les loaders ROM sont **lents** et **standards**. Les éditeurs ont donc développé leurs propres loaders pour :

1. **Accélérer le chargement** (×2 à ×10)
2. **Protéger le logiciel** (format non standard, checksums, timings)
3. **Afficher des écrans de chargement animés** (loading screens)

C'est la naissance des **loaders propriétaires**, qui sont à la fois des outils de performance et des outils de protection.

---

## 3. Les loaders « officiels » (ROM) : la base commune {#3-loaders-officiels}

### 3.1 Tableau comparatif

| Plateforme | Loader ROM | Débit | Temps de chargement (40 Ko) | Particularités |
| --- | --- | --- | --- | --- |
| C64 (datasette) | FSK 1480/833 Hz | ≈ 300 bauds | ≈ 18 min | Datasette dédiée, port série |
| ZX Spectrum | FSK 2400/1200 Hz | 1200 bauds | ≈ 4-5 min | Magnétophone standard |
| CPC 464 | FSK 2000/1000 Hz | ≈ 1000 bauds | ≈ 5-6 min | Magnétophone intégré |
| ZX81 | FSK 300/1500 Hz | 300/1500 bauds | ≈ 20 min | Très lent |
| Oric | FSK 300/2400 Hz | 300/2400 bauds | ≈ 4-5 min | Compatible Spectrum |
| Thomson TO7 | FSK propriétaire | ≈ 1200 bauds | ≈ 5 min | Format maison |
| MSX | FSK 1200 Hz | 1200 bauds | ≈ 4-5 min | Standard Yamaha |
| BBC Micro | FSK 300/1200 Hz | 300/1200 bauds | ≈ 5 min | Mode haut/bas débit |
| Atari 8 bits | SIO (série) | ≈ 600 bauds | ≈ 10 min | Protocole série propriétaire |

### 3.2 Le format standard : blocs et checksums

Tous les loaders ROM utilisent une structure similaire :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  STRUCTURE D'UN BLOC K7 (loader ROM)                         │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Pilote (sync) : longue séquence de bits identiques       │
 │     (permet au loader de se synchroniser sur le signal)      │
 │  2. En-tête : nom du fichier, taille, type                   │
 │  3. Données : le contenu du fichier                          │
 │  4. Checksum : somme de contrôle (XOR ou somme modulo 256)   │
 │  5. Silence : pause entre blocs                              │
 └──────────────────────────────────────────────────────────────┘
```

**Exemple C64 (loader ROM)** :

```
 Pilote : 9 secondes de bits à 1480 Hz (sync)
 En-tête : type (1 o) + nom (16 o) + taille (2 o)
 Données : N octets
 Checksum : XOR de tous les octets (1 o)
```

### 3.3 Les limites du loader ROM

| Limite | Conséquence |
| --- | --- |
| **Lent** | 300-1200 bauds, temps de chargement longs |
| **Standard** | Tout le monde peut copier avec un loader ROM |
| **Pas de protection** | Aucun mécanisme anti-copie |
| **Pas d'écran animé** | L'écran reste noir ou affiche un message statique |

C'est pourquoi les éditeurs ont développé leurs propres loaders.

---

## 4. Les loaders propriétaires des éditeurs {#4-loaders-proprietaires}

### 4.1 Pourquoi des loaders propriétaires ?

Les loaders propriétaires répondent à trois besoins :

1. **Accélérer le chargement** : ×2 à ×10 par rapport au loader ROM
2. **Protéger le logiciel** : format non standard, difficile à copier
3. **Personnaliser l'expérience** : écrans de chargement animés, musiques

### 4.2 Les grands loaders propriétaires par plateforme

#### 4.2.1 Commodore 64

| Loader | Éditeur | Année | Débit | Particularités |
| --- | --- | --- | --- | --- |
| **TurboTape** | Divers | ≈ 1985 | ×3-5 | Loader rapide, format propriétaire |
| **SeaSucker** | Ocean Software | ≈ 1986 | ×4 | Loader très rapide, écran animé |
| **Paul Owens' Protection System (POPS)** | POPS | ≈ 1987 | ×3 | Loader + protection |
| **Fireload** | Firebird | ≈ 1987 | ×4 | Loader rapide, checksums |
| **Bleepload** | Divers | ≈ 1988 | ×5 | Loader très rapide |

#### 4.2.2 ZX Spectrum

| Loader | Éditeur | Année | Débit | Particularités |
| --- | --- | --- | --- | --- |
| **Speedlock 1-7** | Speedlock | 1985-1991 | ×3-8 | Loader + protection (voir §5) |
| **Alkatraz** | Alkatraz | ≈ 1986 | ×4 | Loader rapide, format propriétaire |
| **Paul Owens' Protection System (POPS)** | POPS | ≈ 1987 | ×3 | Loader + protection |
| **Fireload** | Firebird | ≈ 1987 | ×4 | Loader rapide, checksums |
| **Bleepload** | Divers | ≈ 1988 | ×5 | Loader très rapide |
| **Datasoft Loader** | Datasoft | ≈ 1986 | ×3 | Loader propriétaire |

#### 4.2.3 Amstrad CPC

| Loader | Éditeur | Année | Débit | Particularités |
| --- | --- | --- | --- | --- |
| **Speedlock CPC** | Speedlock | 1986-1991 | ×3-6 | Loader + protection |
| **Alkatraz CPC** | Alkatraz | ≈ 1987 | ×4 | Loader rapide |
| **Datasoft CPC** | Datasoft | ≈ 1986 | ×3 | Loader propriétaire |

#### 4.2.4 Autres plateformes

| Plateforme | Loader | Particularités |
| --- | --- | --- |
| Oric | **Hyperload** | Loader rapide, format propriétaire |
| Thomson | **Loader Thomson** | Format maison, protégé |
| MSX | **MSX Turbo** | Loader rapide, compatible Yamaha |
| BBC Micro | **BBC Fast Loader** | Loader rapide, format propriétaire |

### 4.3 Anatomie d'un loader propriétaire

Un loader propriétaire typique comprend :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ANATOMIE D'UN LOADER PROPRIÉTAIRE                           │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Routine de synchronisation                               │
 │     - Détection du pilote (sync)                             │
 │     - Calibration de la vitesse (optionnel)                  │
 │                                                              │
 │  2. Routine de décodage                                      │
 │     - Lecture du signal audio                                │
 │     - Conversion en bits (FSK, Manchester, etc.)             │
 │     - Gestion des erreurs (retry, skip)                      │
 │                                                              │
 │  3. Routine de vérification                                  │
 │     - Checksum (XOR, somme, CRC)                             │
 │     - Validation de l'en-tête                                │
 │                                                              │
 │  4. Routine de chargement                                    │
 │     - Écriture des données en mémoire                        │
 │     - Gestion des blocs multiples                            │
 │                                                              │
 │  5. Routine de protection (optionnel)                        │
 │     - Timings (mesure du temps de chargement)                │
 │     - Auto-modification (le loader se modifie lui-même)      │
 │     - Anti-debug (détection de freezer)                      │
 └──────────────────────────────────────────────────────────────┘
```

### 4.4 Zoom : Speedlock (Spectrum et CPC)

**Speedlock** est **le loader propriétaire le plus célèbre** des années 1980, développé par **Speedlock Associates** (Royaume-Uni). Il a connu **7 générations** successives, chacune ajoutant des couches de protection.

```mermaid
flowchart TD
    A["Speedlock 1 (1985)"] --> B["Loader rapide<br/>format propriétaire"]
    B --> C["Speedlock 2 (1986)"]
    C --> D["+ anti-debug<br/>détection de freezer"]
    D --> E["Speedlock 3 (1987)"]
    E --> F["+ protection par timing<br/>mesure du temps de chargement"]
    F --> G["Speedlock 4 (1988)"]
    G --> H["+ checksums dynamiques<br/>vérification du code en mémoire"]
    H --> I["Speedlock 5 (1989)"]
    I --> J["+ auto-modification<br/>le loader se modifie lui-même"]
    J --> K["Speedlock 6 (1990)"]
    K --> L["+ timings avancés<br/>mesure entre blocs"]
    L --> M["Speedlock 7 (1991)"]
    M --> N["+ obfuscation<br/>code difficile à désassembler"]
    style B fill:#1e3a5f,color:#fff
    style D fill:#5f1e1e,color:#fff
    style F fill:#5f3a1e,color:#fff
    style H fill:#5f5f1e,color:#fff
    style J fill:#3a5f1e,color:#fff
    style L fill:#1e5f3a,color:#fff
    style N fill:#1e3a5f,color:#fff
```

```
 ┌──────────────────────────────────────────────────────────────┐
 │  SPEEDLOCK (générations)                                     │
 ├──────────────────────────────────────────────────────────────┤
 │  Speedlock 1 (1985) :                                        │
 │  • Loader rapide (×3-5 par rapport au ROM)                   │
 │  • Format propriétaire (FSK modifié)                         │
 │  • Écran de chargement animé                                 │
 │                                                              │
 │  Speedlock 2 (1986) :                                        │
 │  • + anti-debug : détection de la présence d'un freezer      │
 │    (Multiface, etc.) via vérification des vecteurs NMI       │
 │                                                              │
 │  Speedlock 3 (1987) :                                        │
 │  • + protection par timing : mesure du temps de chargement   │
 │    d'un bloc. Si trop rapide (copie numérique), échec        │
 │                                                              │
 │  Speedlock 4 (1988) :                                        │
 │  • + checksums dynamiques : vérification du code en mémoire  │
 │    après chargement. Si modifié (crack), échec               │
 │                                                              │
 │  Speedlock 5 (1989) :                                        │
 │  • + auto-modification : le loader se modifie lui-même       │
 │    pendant le chargement, rendant le désassemblage difficile │
 │                                                              │
 │  Speedlock 6 (1990) :                                        │
 │  • + timings avancés : mesure du temps entre plusieurs blocs │
 │    (pas seulement un bloc)                                   │
 │                                                              │
 │  Speedlock 7 (1991) :                                        │
 │  • + obfuscation : code rendu difficile à lire (junk code,   │
 │    sauts imbriqués, calculs redondants)                      │
 └──────────────────────────────────────────────────────────────┘
```

**Impact** : Speedlock a été utilisé par des centaines de jeux Spectrum et CPC (Ocean, US Gold, Codemasters, etc.). Il a été **systématiquement cracké** par la scène, mais chaque génération a nécessité de nouvelles techniques.

---

## 5. Les protections spécifiques K7 {#5-protections-specifiques}

### 5.1 Pourquoi les protections K7 sont différentes des protections disquette

| Protection disquette | Protection K7 |
| --- | --- |
| **Weak bits** (zone sans flux) | ❌ Impossible (support linéaire, pas de flux magnétique aléatoire) |
| **Long tracks** (piste > 100 %) | ❌ Impossible (pas de pistes, juste une bande linéaire) |
| **CRC faux** | ✅ Possible (checksum volontairement faux) |
| **Secteurs hors-norme** | ❌ Impossible (pas de secteurs) |
| **Timings** | ✅ Possible (mesure du temps de chargement) |
| **Anti-debug** | ✅ Possible (détection de freezer) |
| **Auto-modification** | ✅ Possible (le loader se modifie) |
| **Silences** | ✅ Possible (zones de silence entre blocs) |

### 5.2 Les protections par timing

**Principe** : le loader mesure le **temps de chargement** d'un bloc. Si le temps est trop court (copie numérique, fast loader), la protection échoue.

```mermaid
flowchart TD
    A["Chargement d'un bloc"] --> B["Mesure du temps<br/>(compteur VBL, timer)"]
    B --> C{"Temps < seuil ?"}
    C -->|"oui"| D["Copie numérique détectée<br/>protection activée"]
    C -->|"non"| E["Chargement normal<br/>jeu lancé"]
    D --> F["Écran de piratage<br/>ou boucle infinie"]
    style D fill:#5f1e1e,color:#fff
```

**Contre-mesure** : le cracker doit **patcher la routine de mesure** pour qu'elle retourne toujours un temps « normal », ou **désactiver le fast loader** pendant le chargement.

### 5.3 Les protections par checksums dynamiques

**Principe** : après chargement, le programme vérifie que le code en mémoire n'a pas été modifié (par un crack).

```
 ┌──────────────────────────────────────────────────────────────┐
 │  PROTECTION PAR CHECKSUM DYNAMIQUE                           │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Le programme calcule la somme de contrôle du code chargé │
 │  2. Il compare avec une valeur attendue                      │
 │  3. Si la somme diffère (code modifié), le programme réagit  │
 │     (écran de piratage, boucle infinie)                      │
 └──────────────────────────────────────────────────────────────┘
```

**Contre-mesure** : le cracker doit **recalculer le checksum** après modification, ou **patcher le test**.

### 5.4 Les protections par auto-modification

**Principe** : le loader **se modifie lui-même** pendant le chargement. Cela rend le désassemblage statique inefficace.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  PROTECTION PAR AUTO-MODIFICATION                            │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Le loader contient du code « mort » (inintelligible)     │
 │  2. Pendant le chargement, il s'auto-modifie pour devenir    │
 │     exécutable                                               │
 │  3. Un désassembleur statique ne voit que du code mort       │
 │  4. Il faut exécuter le loader pas-à-pas pour le comprendre  │
 └──────────────────────────────────────────────────────────────┘
```

**Contre-mesure** : désassemblage dynamique (pas-à-pas), ou gel après auto-modification.

### 5.5 Les protections par silences

**Principe** : des **zones de silence** sont insérées entre les blocs. Le loader mesure la durée du silence. Si trop court (copie numérique qui supprime les silences), la protection échoue.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  PROTECTION PAR SILENCES                                     │
 ├──────────────────────────────────────────────────────────────┤
 │  Bloc 1 ─── [SILENCE 2s] ─── Bloc 2 ─── [SILENCE 3s] ───   │
 │                                                              │
 │  Le loader mesure la durée du silence.                       │
 │  Si < 1,5s → copie détectée                                  │
 └──────────────────────────────────────────────────────────────┘
```

**Contre-mesure** : le cracker doit **préserver les silences** lors de la copie, ou **patcher la mesure**.

### 5.6 Les protections par anti-debug

**Principe** : le loader détecte la présence d'un **freezer** (Multiface, Action Replay) et réagit.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  PROTECTION PAR ANTI-DEBUG                                   │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Le loader vérifie les vecteurs d'interruption (NMI, IRQ) │
 │  2. Si un vecteur a été détourné (freezer actif), le loader  │
 │     réagit (écran de piratage)                               │
 │  3. Ou : le loader mesure le temps entre deux instructions   │
 │     (un freezer ralentit l'exécution)                        │
 └──────────────────────────────────────────────────────────────┘
```

**Contre-mesure** : désactiver la cartouche (Final Kill), ou patcher le test.

### 5.7 Les protections par format propriétaire

**Principe** : le loader utilise un **format de données non standard** (FSK modifié, Manchester, etc.) que le loader ROM ne sait pas lire.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  PROTECTION PAR FORMAT PROPRIÉTAIRE                          │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Le loader utilise une modulation non standard            │
 │     (ex : FSK avec fréquences différentes du ROM)            │
 │  2. Une copie K7→K7 avec un loader ROM échoue                │
 │  3. Il faut utiliser le loader propriétaire pour copier      │
 └──────────────────────────────────────────────────────────────┘
```

**Contre-mesure** : le cracker doit **dumper le signal** (voir §6), ou **copier avec le bon loader**.

### 5.8 Tableau récapitulatif

| Protection | Principe | Détectée par… | Contre-mesure |
| --- | --- | --- | --- |
| **Timing** | Mesure du temps de chargement | Compteur VBL, timer | Patch de la mesure, désactivation fast loader |
| **Checksum dynamique** | Vérification du code en mémoire | Somme de contrôle | Recalcul du checksum, patch du test |
| **Auto-modification** | Le loader se modifie lui-même | Exécution pas-à-pas | Désassemblage dynamique |
| **Silences** | Zones de silence entre blocs | Mesure de durée | Préservation des silences, patch |
| **Anti-debug** | Détection de freezer | Vecteurs d'interruption | Désactivation cartouche (Final Kill) |
| **Format propriétaire** | Modulation non standard | Loader ROM | Dump numérique, copie avec bon loader |

---

## 6. Les outils des crackers : copier, dumper, accélérer {#6-outils-crackers}

### 6.1 La copie K7→K7

**Principe** : copier une K7 protégée sur une autre K7, en utilisant deux magnétophones.

```mermaid
flowchart TD
    A["K7 originale<br/>(loader propriétaire)"] --> B["Lecture sur magnétophone 1"]
    B --> C["Enregistrement sur magnétophone 2"]
    C --> D{"Copie réussie ?"}
    D -->|"oui"| E["Test de la copie"]
    D -->|"non"| F{"Protection par format ?"}
    F -->|"oui"| G["Copie impossible avec loader ROM<br/>il faut le loader propriétaire"]
    F -->|"non"| H{"Protection par timing ?"}
    H -->|"oui"| I["Copie dégradée<br/>(timings altérés)"]
    H -->|"non"| J["Copie OK"]
    style G fill:#5f1e1e,color:#fff
    style I fill:#5f3a1e,color:#fff
```

**Limites** :

- La copie K7→K7 **dégrade le signal** (bruit, distorsion)
- Les protections par **timing** peuvent échouer (vitesse variable des magnétophones)
- Les protections par **format propriétaire** nécessitent le bon loader

### 6.2 Le dump numérique

**Principe** : convertir le signal audio de la K7 en **fichier numérique** (WAV, TAP, TZX, etc.) pour le préserver ou le copier sans dégradation.

```mermaid
flowchart TD
    A["K7 originale"] --> B["Lecture sur magnétophone"]
    B --> C["Signal audio (ligne out)"]
    C --> D["Carte son PC (entrée ligne)"]
    D --> E["Enregistrement WAV"]
    E --> F{"Conversion en format<br/>de préservation ?"}
    F -->|"oui"| G["Outil de conversion<br/>(MakeTZX, TapOrac, etc.)"]
    G --> H["Fichier TAP / TZX / CDT"]
    F -->|"non"| I["Fichier WAV brut"]
    style G fill:#1e3a5f,color:#fff
```

**Outils de dump** :

| Plateforme | Outil | Format produit |
| --- | --- | --- |
| C64 | **TapEx**, **C64 Tape DIY** | TAP |
| Spectrum | **MakeTZX**, **Tape2Wav**, **TZX tools** | TZX, WAV |
| CPC | **MakeCDT**, **CPC Tape DIY** | CDT |
| Multi | **KryoFlux** (mode audio) | Flux brut |

### 6.3 Les fast loaders

**Principe** : des routines logicielles qui **accélèrent le chargement** depuis la K7, en contournant le loader ROM.

| Plateforme | Fast loader | Débit | Particularités |
| --- | --- | --- | --- |
| C64 | **TurboTape**, **SeaSucker** | ×3-5 | Loader rapide, format propriétaire |
| Spectrum | **Speedlock**, **Alkatraz** | ×3-8 | Loader rapide, protection |
| CPC | **Speedlock CPC**, **Alkatraz CPC** | ×3-6 | Loader rapide, protection |

**Attention** : les fast loaders peuvent être **détectés par les protections par timing**.

### 6.4 Les cracktros sur K7

**Principe** : ajouter une **intro de groupe** (cracktro) avant le jeu, sur la même K7.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  STRUCTURE D'UNE K7 CRACKÉE                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Cracktro (loader + musique + scroll + logo)              │
 │  2. Jeu (loader propriétaire ou ROM)                         │
 │                                                              │
 │  La cracktro est chargée en premier, puis le jeu             │
 └──────────────────────────────────────────────────────────────┘
```

### 6.5 Le tape trading

**Principe** : échanger des K7 crackées entre membres de la scène, par courrier postal ou lors de rencontres.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  LE TAPE TRADING                                             │
 ├──────────────────────────────────────────────────────────────┤
 │  1. Un cracker crack un jeu et l'enregistre sur K7           │
 │  2. Il envoie la K7 à un « courier »                         │
 │  3. Le courier la copie et l'envoie à d'autres membres       │
 │  4. La K7 circule dans la scène (swapping postal)            │
 │                                                              │
 │  La qualité se dégrade à chaque copie (bruit, distorsion)    │
 └──────────────────────────────────────────────────────────────┘
```

---

## 7. Études de cas par plateforme {#7-etudes-de-cas}

### 7.1 Commodore 64 : TurboTape et les loaders Ocean

**TurboTape** (≈ 1985) est l'un des premiers loaders propriétaires C64. Il utilise une modulation FSK modifiée pour accélérer le chargement (×3-5).

```
 ┌──────────────────────────────────────────────────────────────┐
 │  TURBOTAPE (C64)                                             │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader rapide (×3-5 par rapport au ROM)                   │
 │  • Format FSK modifié (fréquences différentes)               │
 │  • Écran de chargement animé                                 │
 │  • Pas de protection avancée                                 │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie avec un loader TurboTape                            │
 │  • Dump numérique (TAP)                                      │
 └──────────────────────────────────────────────────────────────┘
```

**Ocean Software** a utilisé **SeaSucker** (≈ 1986), un loader très rapide (×4) avec écrans de chargement animés célèbres (le « Ocean Loader » avec musique de Martin Galway).

```
 ┌──────────────────────────────────────────────────────────────┐
 │  OCEAN LOADER (SeaSucker)                                    │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader très rapide (×4)                                   │
 │  • Écran de chargement animé (scroll, musique)               │
 │  • Musique de Martin Galway (célèbre)                        │
 │  • Format propriétaire                                       │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie avec loader SeaSucker                               │
 │  • Dump numérique (TAP)                                      │
 └──────────────────────────────────────────────────────────────┘
```

### 7.2 ZX Spectrum : Speedlock et POPS

**Speedlock** (voir §4.4) a été le loader propriétaire le plus utilisé sur Spectrum. Ses 7 générations ont représenté un défi constant pour les crackers.

**POPS (Paul Owens' Protection System)** (≈ 1987) est un autre loader propriétaire célèbre, utilisé par des éditeurs comme **Codemasters**.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  POPS (Paul Owens' Protection System)                        │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader rapide (×3)                                        │
 │  • Format propriétaire                                       │
 │  • Protection par checksum                                   │
 │  • Écran de chargement animé                                 │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie avec loader POPS                                    │
 │  • Dump numérique (TZX)                                      │
 │  • Patch du checksum                                         │
 └──────────────────────────────────────────────────────────────┘
```

### 7.3 Amstrad CPC : Speedlock CPC et Alkatraz

**Speedlock CPC** est l'adaptation du Speedlock Spectrum au CPC. Il utilise les mêmes techniques (timings, checksums, anti-debug).

**Alkatraz CPC** (≈ 1987) est un loader rapide (×4) avec format propriétaire.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ALKATRAZ CPC                                                │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader rapide (×4)                                        │
 │  • Format propriétaire                                       │
 │  • Écran de chargement animé                                 │
 │  • Pas de protection avancée                                 │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie avec loader Alkatraz                                │
 │  • Dump numérique (CDT)                                      │
 └──────────────────────────────────────────────────────────────┘
```

### 7.4 ZX81 : le loader ultra-lent

Le ZX81 utilise un loader ROM **très lent** (300/1500 bauds), ce qui rend le chargement d'un jeu de 16 Ko très long (≈ 20 minutes).

```
 ┌──────────────────────────────────────────────────────────────┐
 │  ZX81 ROM LOADER                                             │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader très lent (300/1500 bauds)                         │
 │  • Format FSK standard                                       │
 │  • Pas de protection                                         │
 │  • Temps de chargement : ≈ 20 min pour 16 Ko                 │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie K7→K7 triviale                                      │
 │  • Dump numérique (P)                                        │
 └──────────────────────────────────────────────────────────────┘
```

### 7.5 Oric : Hyperload

**Hyperload** est un loader rapide pour Oric (×3-5), avec format propriétaire.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  HYPERLOAD (Oric)                                            │
 ├──────────────────────────────────────────────────────────────┤
 │  • Loader rapide (×3-5)                                      │
 │  • Format propriétaire                                       │
 │  • Écran de chargement animé                                 │
 │                                                              │
 │  Contre-mesure :                                             │
 │  • Copie avec loader Hyperload                               │
 │  • Dump numérique                                            │
 └──────────────────────────────────────────────────────────────┘
```

---

## 8. La culture du chargement : bruits, écrans, temps {#8-culture-chargement}

### 8.1 Les bruits caractéristiques

Chaque loader a un **bruit caractéristique** (le son du signal audio). Ces bruits sont devenus iconiques :

| Loader | Bruit caractéristique |
| --- | --- |
| C64 ROM | Grésillement continu (FSK 1480/833 Hz) |
| Spectrum ROM | Sifflement aigu (FSK 2400/1200 Hz) |
| Speedlock | Sifflement modulé (FSK modifié) |
| Ocean Loader | Sifflement + musique (Martin Galway) |
| Alkatraz | Grésillement rapide |

Ces bruits sont **reproduits dans les émulateurs** pour l'authenticité.

### 8.2 Les écrans de chargement (loading screens)

Les loaders propriétaires affichent souvent des **écrans de chargement animés** pendant le chargement :

```
 ┌──────────────────────────────────────────────────────────────┐
 │  LOADING SCREENS                                             │
 ├──────────────────────────────────────────────────────────────┤
 │  • Écrans fixes (logo de l'éditeur, nom du jeu)              │
 │  • Écrans animés (scroll, effets graphiques)                 │
 │  • Écrans avec musique (SID sur C64, AY sur Spectrum/CPC)    │
 │                                                              │
 │  Exemples célèbres :                                         │
 │  • Ocean Loader (C64) : scroll + musique de Martin Galway    │
 │  • Speedlock (Spectrum) : écran animé avec musique           │
 │  • US Gold (C64) : écrans avec musique de Rob Hubbard        │
 └──────────────────────────────────────────────────────────────┘
```

### 8.3 Les temps de chargement

Les temps de chargement variaient énormément selon le loader et la taille du jeu :

| Loader | Débit | Temps (40 Ko) |
| --- | --- | --- |
| C64 ROM | 300 bauds | ≈ 18 min |
| Spectrum ROM | 1200 bauds | ≈ 4-5 min |
| CPC ROM | 1000 bauds | ≈ 5-6 min |
| TurboTape (C64) | ×3-5 | ≈ 4-6 min |
| Speedlock (Spectrum) | ×3-8 | ≈ 1-2 min |
| SeaSucker (C64) | ×4 | ≈ 4-5 min |

### 8.4 Le « PRESS PLAY ON TAPE »

Le message **« PRESS PLAY ON TAPE »** (ou **« PRESS PLAY »**) est l'invite affichée par le loader ROM pour demander à l'utilisateur de lancer la lecture de la K7. Ce message est devenu **iconique** et est souvent reproduit dans les jeux modernes (hommages, rétros).

```
 ┌──────────────────────────────────────────────────────────────┐
 │                                                              │
 │                    PRESS PLAY ON TAPE                        │
 │                                                              │
 │                       THEN PRESS ANY KEY                     │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

### 8.5 Les multi-chargements

Beaucoup de jeux K7 sont **multi-chargements** : le jeu recharge du code en cours de partie (niveaux, écrans, etc.). Cela nécessite de **revenir à la K7** et de rebobiner pour trouver le bon bloc.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  MULTI-CHARGEMENT K7                                         │
 ├──────────────────────────────────────────────────────────────┤
 │  Bloc 1 : Niveau 1                                           │
 │  Bloc 2 : Niveau 2                                           │
 │  Bloc 3 : Niveau 3                                           │
 │  ...                                                         │
 │                                                              │
 │  Le jeu affiche : "PLAY SIDE 2" ou "REWIND TAPE"             │
 │  L'utilisateur doit retrouver le bon bloc sur la K7          │
 └──────────────────────────────────────────────────────────────┘
```

---

## 9. La préservation moderne : du TAP au TZX {#9-preservation-moderne}

### 9.1 Les formats de préservation

| Format | Plateforme | Niveau | Contenu | Préserve les protections ? |
| --- | --- | --- | --- | --- |
| **TAP** | C64 | Logique | Blocs de données (en-tête + données + checksum) | Non (seulement les données) |
| **TZX** | Spectrum, CPC, autres | Logique+ | Blocs de données + timings + silences + formats propriétaires | Oui (en grande partie) |
| **CDT** | CPC | Logique+ | Similaire à TZX, adapté au CPC | Oui |
| **PZX** | Spectrum | Physique | Flux de bits (plus précis que TZX) | Oui (intégralement) |
| **WAV** | Multi | Physique | Signal audio brut | Oui (intégralement, mais volumineux) |
| **CAS** | Atari 8 bits | Logique | Blocs de données | Partiellement |

### 9.2 Le format TAP (C64)

**TAP** est le format de préservation le plus ancien pour le C64 (≈ 1992). Il stocke les **blocs de données** (en-tête + données + checksum) tels qu'ils sont lus par le loader ROM ou un loader propriétaire.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  FORMAT TAP                                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  En-tête fichier :                                           │
 │  • Signature : "C64-TAPE-RAW"                                │
 │  • Version : 0 ou 1                                          │
 │                                                              │
 │  Blocs :                                                     │
 │  • Longueur du bloc (3 octets)                               │
 │  • Données du bloc (en-tête + données + checksum)            │
 │  • Flags (optionnel, version 1)                              │
 └──────────────────────────────────────────────────────────────┘
```

**Limites** : TAP ne préserve pas les **timings** ni les **silences**, donc certaines protections échouent.

### 9.3 Le format TZX (Spectrum, multi-plateformes)

**TZX** (≈ 1995) est un format beaucoup plus riche, capable de stocker :

- Des **blocs de données standards** (ROM loader)
- Des **blocs de données turbo** (loaders propriétaires)
- Des **silences** (pauses entre blocs)
- Des **tones pilotes** (sync)
- Des **séquences de bits brutes** (pour les formats exotiques)
- Des **informations de protection** (timings, checksums)

```
 ┌──────────────────────────────────────────────────────────────┐
 │  FORMAT TZX                                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  En-tête fichier :                                           │
 │  • Signature : "ZXTape!"                                     │
 │  • Version : 1.13                                            │
 │                                                              │
 │  Blocs (types multiples) :                                   │
 │  • 0x10 : Standard speed data block (ROM loader)             │
 │  • 0x11 : Turbo speed data block (loader propriétaire)       │
 │  • 0x12 : Pure tone (pilote)                                 │
 │  • 0x13 : Pulse sequence                                     │
 │  • 0x14 : Pure data block                                    │
 │  • 0x15 : Direct recording (flux brut)                       │
 │  • 0x20 : Pause (silence)                                    │
 │  • 0x21 : Group start (nom de groupe)                        │
 │  • 0x30 : Text description                                   │
 │  • 0x31 : Message block                                      │
 │  • 0x32 : Archive info (métadonnées)                         │
 │  • ...                                                       │
 └──────────────────────────────────────────────────────────────┘
```

**Avantages** : TZX préserve la **plupart des protections** (timings, silences, formats propriétaires).

### 9.4 Le format CDT (CPC)

**CDT** est l'adaptation du format TZX au CPC. Il utilise la même structure, mais avec des blocs adaptés au loader CPC.

### 9.5 Le format PZX (Spectrum, moderne)

**PZX** (≈ 2010s) est un format plus récent et plus précis que TZX. Il stocke le **flux de bits** (pulses) avec une résolution temporelle très fine.

```
 ┌──────────────────────────────────────────────────────────────┐
 │  FORMAT PZX                                                  │
 ├──────────────────────────────────────────────────────────────┤
 │  • Stocke les pulses (transitions) avec résolution 1/3,5 MHz │
 │  • Préserve intégralement le signal                          │
 │  • Plus précis que TZX pour les protections complexes        │
 └──────────────────────────────────────────────────────────────┘
```

### 9.6 Les outils de dump modernes

| Outil | Plateforme | Format produit | Particularités |
| --- | --- | --- | --- |
| **MakeTZX** | Spectrum | TZX | Conversion WAV → TZX |
| **TapEx** | C64 | TAP | Dump depuis datasette |
| **CPC Tape DIY** | CPC | CDT | Dump depuis magnétophone |
| **KryoFlux** (mode audio) | Multi | WAV, flux brut | Dump haute précision |
| **TZX tools** | Spectrum | TZX | Édition, conversion |

### 9.7 Les émulateurs et la lecture K7

Les émulateurs modernes (VICE, Fuse, CPCEmu, etc.) peuvent lire les fichiers TAP, TZX, CDT, PZX et **simuler le chargement** comme si la K7 était insérée dans un vrai magnétophone.

```mermaid
flowchart TD
    A["Fichier TAP/TZX/CDT/PZX"] --> B["Émulateur (VICE, Fuse, CPCEmu)"]
    B --> C["Simulation du loader ROM ou propriétaire"]
    C --> D["Chargement du jeu en mémoire"]
    D --> E["Exécution du jeu"]
    style B fill:#1e3a5f,color:#fff
```

---

## 10. Conclusion {#10-conclusion}

Les protections sur K7 et les loaders associés représentent un **chapitre fascinant** de l'histoire de l'informatique. Loin d'être un support « pauvre » par rapport à la disquette, la cassette a été le **vecteur principal** de distribution des logiciels pendant plus de 10 ans (1980-1990), et a donné naissance à une **culture spécifique** :

- **Les bruits caractéristiques** des loaders (grésillements, sifflements)
- **Les écrans de chargement animés** (loading screens)
- **Les temps de chargement** (de 1 à 20 minutes)
- **Le « PRESS PLAY ON TAPE »** iconique
- **Les multi-chargements** (rewind tape, play side 2)

Les protections K7 sont **fondamentalement différentes** des protections disquette : pas de weak bits, pas de long tracks, mais des **timings**, des **checksums**, des **silences**, de l'**auto-modification**, et de l'**anti-debug**. Les loaders propriétaires (Speedlock, Alkatraz, TurboTape, SeaSucker) ont été à la fois des **outils de performance** (chargement rapide) et des **outils de protection** (format propriétaire).

Les crackers ont répondu avec des **outils de copie** (K7→K7, dump numérique), des **fast loaders**, et des **cracktros** ajoutées aux jeux. Le **tape trading** a été un réseau de distribution mondial, avant l'ère d'Internet.

Aujourd'hui, les formats de préservation (TAP, TZX, CDT, PZX) permettent de **sauvegarder intégralement** ces logiciels, avec leurs protections, leurs timings, et leurs écrans de chargement. Les émulateurs modernes peuvent **simuler fidèlement** l'expérience de chargement, bruits inclus.

L'héritage de cette époque est double :

1. **Culturel** : les bruits, les écrans, les temps de chargement font partie de la mémoire collective des joueurs des années 1980.
2. **Technique** : les loaders propriétaires ont posé les bases des formats de compression et de protection modernes.

---

## Annexes

### Annexe A — Tableau comparatif des principaux loaders

| Loader | Plateforme | Type | Année | Débit | Particularités |
| --- | --- | --- | --- | --- | --- |
| C64 ROM | C64 | Officiel (ROM) | 1982 | 300 bauds | Datasette, FSK 1480/833 Hz |
| Spectrum ROM | Spectrum | Officiel (ROM) | 1982 | 1200 bauds | FSK 2400/1200 Hz |
| CPC ROM | CPC | Officiel (ROM) | 1984 | 1000 bauds | FSK 2000/1000 Hz |
| TurboTape | C64 | Propriétaire | ≈ 1985 | ×3-5 | Loader rapide, format FSK modifié |
| SeaSucker (Ocean) | C64 | Propriétaire | ≈ 1986 | ×4 | Loader rapide, écran animé, musique |
| Speedlock 1-7 | Spectrum, CPC | Propriétaire + protection | 1985-1991 | ×3-8 | Loader + timings + checksums + anti-debug |
| Alkatraz | Spectrum, CPC | Propriétaire | ≈ 1986-1987 | ×4 | Loader rapide, format propriétaire |
| POPS | Spectrum | Propriétaire + protection | ≈ 1987 | ×3 | Loader + checksums |
| Fireload | Spectrum, CPC | Propriétaire | ≈ 1987 | ×4 | Loader rapide, checksums |
| Bleepload | Spectrum | Propriétaire | ≈ 1988 | ×5 | Loader très rapide |
| Datasoft | Spectrum, CPC | Propriétaire | ≈ 1986 | ×3 | Loader propriétaire |
| Hyperload | Oric | Propriétaire | ≈ 1985 | ×3-5 | Loader rapide |
| MSX Turbo | MSX | Propriétaire | ≈ 1985 | ×3-5 | Loader rapide, compatible Yamaha |

### Annexe B — Glossaire étendu

| Terme | Définition |
| --- | --- |
| **Baud** | Unité de mesure de la vitesse de transmission (bits par seconde) |
| **CDT** | Format de préservation pour Amstrad CPC (similaire à TZX) |
| **Checksum** | Somme de contrôle pour vérifier l'intégrité des données |
| **Cracktro** | Intro de signature d'un groupe, ajoutée au jeu craqué |
| **Datasette** | Lecteur de cassette dédié (C64) |
| **Dump** | Conversion d'un support physique en fichier numérique |
| **Fast loader** | Routine logicielle accélérant le chargement |
| **FSK** | Frequency Shift Keying : modulation par changement de fréquence |
| **Loading screen** | Écran affiché pendant le chargement |
| **Multi-chargement** | Jeu qui recharge du code en cours de partie |
| **PZX** | Format de préservation moderne pour Spectrum (flux de bits) |
| **Silence** | Zone de bande sans signal audio |
| **TAP** | Format de préservation pour C64 (blocs de données) |
| **Tape trading** | Échange de K7 crackées entre membres de la scène |
| **Timing** | Mesure du temps de chargement (protection) |
| **TZX** | Format de préservation pour Spectrum et autres (blocs + timings) |
| **WAV** | Format audio numérique (signal brut) |

### Annexe C — Errata et points à vérifier

| # | Passage | Correction | Justification |
| --- | --- | --- | --- |
| 1 | Speedlock « uniquement Spectrum » | Speedlock existe aussi sur **CPC** et **C64** (versions différentes) | Portages |
| 2 | POPS « uniquement Spectrum » | POPS existe aussi sur **CPC** | Portages |
| 3 | TZX « uniquement Spectrum » | TZX supporte aussi **CPC, C64, MSX, Atari 8 bits, etc.** | Format multi-plateformes |
| 4 | « Les weak bits sont impossibles sur K7 » | Les weak bits sont impossibles sur K7 car le support est **linéaire** (pas de flux magnétique aléatoire) | Nuance technique |
| 5 | « La copie K7→K7 est toujours possible » | La copie K7→K7 peut échouer si la protection utilise un **format propriétaire** (il faut le bon loader) | Nuance de protection |

### Annexe D — Pour aller plus loin

**Ouvrages et documentations d'époque** ✅

- *Commodore 64 Programmer's Reference Guide* (Commodore) — chapitre sur la datasette
- *ZX Spectrum Manual* (Sinclair) — chapitre sur le chargement K7
- *Amstrad CPC Manual* (Amstrad) — chapitre sur le magnétophone intégré

**Ressources contemporaines** ✅

- **World of Spectrum** (archive Spectrum) : https://worldofspectrum.org
- **Lemon64** (archive C64) : https://www.lemon64.com
- **CPC-Power** (archive CPC) : https://www.cpc-power.com
- **Software Preservation Society** (SPS) : https://www.softpres.org
- **TZX format specification** : https://www.worldofspectrum.org/faq/reference/tzxformat.htm

**Outils modernes** ✅

- **VICE** (émulateur C64) : https://sourceforge.net/projects/vice-emu
- **Fuse** (émulateur Spectrum) : https://fuse-emulator.sourceforge.net
- **CPCEmu** (émulateur CPC) : https://www.cpc-emu.org
- **MakeTZX** (conversion WAV → TZX) : https://www.worldofspectrum.org
- **KryoFlux** (dump haute précision) : https://www.kryoflux.com

---

**Fin du document.** Les diagrammes Mermaid s'affichent nativement sur GitHub, GitLab, Obsidian, Typora et VS Code (extension Markdown Preview Mermaid). Sur un lecteur qui ne les rend pas, le code Mermaid reste lisible tel quel, et tous les schémas essentiels existent aussi en ASCII.

*Professeur Qwen, signant depuis les tranchées du "PRESS PLAY ON TAPE", octobre 2026.* 📼🎵
