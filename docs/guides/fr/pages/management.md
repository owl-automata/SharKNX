# Page Management

La page Management est dédiée au diagnostic KNX des appareils et des installations domotiques. Elle comporte quatre onglets : **Prog. Mode**, **Devices**, **Line Scan** et **Inspect**.

---

## Onglet Prog. Mode

Cet onglet permet de scanner le bus afin de détecter les appareils dont le mode programmation est actuellement actif.

Appuyez sur le **radar FAB** pour démarrer le scan. L’application écoute les appareils en mode programmation et les affiche sous forme de cartes. La durée du scan et l’intervalle de ping sont configurables dans **Scan Settings** (icône engrenage → Scan settings).

Chaque carte d’appareil découverte comporte deux boutons :

- **Check Info** — ouvre l’onglet Devices avec l’adresse physique de l’appareil préremplie, prête pour une lecture des informations appareil.
- **Comm. Info** — ouvre l’onglet Inspect avec l’adresse préremplie, prête pour la lecture des tables de communication de l’appareil.

Cela permet d’effectuer rapidement un scan puis d’accéder immédiatement à des fonctions de diagnostic KNX plus avancées sur n’importe quel appareil trouvé en mode programmation.

---

## Onglet Devices

L’onglet Devices permet d’exécuter des actions de diagnostic sur n’importe quelle adresse physique d’appareil — qu’elle ait été découverte via un scan ou saisie manuellement.

### Badge Data Secure

En haut de l’onglet, un badge indique si des clés d’appareils KNX Data Secure sont chargées (depuis un fichier `.knxkeys` dans l’onglet Security de la page Discovery). Si aucune clé n’est chargée, le badge est orange. Si des clés sont chargées, le badge est bleu et affiche le nombre d’appareils sécurisés. Un appui sur le badge ouvre une fenêtre avec des détails et un raccourci pour charger un fichier `.knxkeys`.

### Saisie d’adresse

Saisissez une adresse physique KNX dans le champ prévu à cet effet. Appuyez sur l’**icône search** pour parcourir les appareils de votre projet ETS chargé et en sélectionner un directement.

### Actions

Une fois l’adresse saisie, quatre actions sont disponibles :

| Action | Description |
|---|---|
| **Check** | Vérifie si l’appareil est présent et répond sur le bus |
| **Read Info** | Lit les informations détaillées directement depuis l’appareil |
| **Toggle Programming Mode** | Active ou désactive à distance le mode programmation de l’appareil |
| **Restart** | Envoie une commande de redémarrage à l’appareil |

**Read Info** récupère les champs suivants depuis l’appareil :
- Descripteur de l’appareil (par ex. System B)
- État du mode programmation
- Fabricant et numéro de commande
- Version du firmware
- État de chargement et état d’exécution
- Version de l’application
- État des tables d’adresses et d’associations
- Longueur APDU maximale
- Type matériel
- Drapeaux d’erreur et état de l’appareil

---

## Onglet Line Scan

L’onglet Line Scan scanne une ligne KNX afin de détecter tous les appareils présents, indépendamment du contenu de votre projet ETS. Cela est utile pour vérifier une installation domotique, détecter des appareils inattendus ou travailler avec un projet inconnu.

### Carte Scan Settings

Configurez le scan avant de démarrer :

| Setting | Description |
|---|---|
| Area and line | Zone.ligne KNX à scanner (par ex. `1.1`). Utilisez **Choose from project** pour sélectionner une ligne depuis votre projet ETS chargé — cela sélectionne également automatiquement le bon type de média. |
| Medium type | TP, IP ou IoT. Nécessaire pour que l’application sache quelle plage d’adresses appareil interroger. |
| Range | Adresse de début et de fin dans la ligne (0–255). Réduisez la plage pour accélérer le scan ou vérifier un segment spécifique. |

Appuyez sur le **scan FAB** pour démarrer. Le scan peut être arrêté à tout moment avant sa fin.

### Résultats du scan

Les appareils découverts apparaissent sous forme de cartes. La couleur de bordure de la carte indique le type d’appareil :

| Colour | Device type |
|---|---|
| Blue | Coupleur KNX |
| Red | Appareil applicatif standard |
| Green | Appareil KNX Secure |

Un bouton **Read Device Info** apparaît au-dessus de la liste des cartes une fois le scan terminé. Un appui dessus lit les informations appareil (fabricant, numéro de série et autres détails) pour tous les appareils découverts de manière séquentielle — pratique pour obtenir rapidement une vue d’ensemble d’une installation de bâtiments intelligents que vous n’avez pas vous-même configurée.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-line-scan.png" width="320" alt="Line scan tab showing discovered device cards with colour-coded borders and the Read Device Info button" />
</div>

### Device Card Detail Sheet

Appuyez sur une carte d’appareil découverte pour ouvrir sa fiche détaillée. Elle contient :

- Une carte d’informations appareil (remplie si Read Device Info a été exécuté)
- Les quatre mêmes actions de diagnostic que dans l’onglet Devices : **Check**, **Read Info**, **Toggle Programming Mode**, **Restart**
- **Program Address** — ouvre une sous-page permettant de saisir une nouvelle adresse physique (ou d’en rechercher une dans votre projet) puis de la programmer dans l’appareil via l’une des deux méthodes suivantes :
  - **Via programming button** — attend jusqu’à 20 secondes qu’un appareil entre en mode programmation, puis écrit l’adresse. Vérifie également les conflits d’adresses sur l’installation réelle.
  - **Via serial number** — si vous avez déjà lu les informations appareil et disposez du numéro de série, programme l’adresse sans nécessiter d’accès physique au bouton de programmation.
- **Rebuild Communication** — ouvre l’onglet Inspect avec l’adresse de cet appareil préremplie.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-device-card.png" width="320" alt="Line scan device card detail sheet showing diagnostic action buttons and Program Address option" />
</div>

---

## Onglet Inspect

L’onglet Inspect lit directement depuis la mémoire d’un appareil ses tables de communication. Cela permet de reconstruire les objets de communication existants, leurs drapeaux et les adresses de groupe qui leur sont associées — sans nécessiter de projet ETS. C’est la méthode la plus efficace pour comprendre un appareil inconnu ou vérifier un appareil dans un projet que vous n’avez pas créé.

### Lecture d’un appareil

Saisissez l’adresse physique d’un appareil dans le champ de saisie puis appuyez sur **Read**. Une barre de progression affiche l’opération en cours. Une fois terminée, une carte de session apparaît pour l’appareil.

La couleur de bordure de la carte indique le succès ou l’échec de l’opération. Chaque carte affiche :
- Adresse physique de l’appareil
- Descripteur de l’appareil (par ex. System B, coupleur KNX)
- Si les informations complètes de l’appareil ont été lues (affiche alors le fabricant et le numéro de commande)

Un bouton **Read Full Info** sur chaque carte déclenche une lecture séparée des informations appareil si vous souhaitez obtenir les détails complets sans ralentir la reconstruction initiale des tables.

Les cartes de session sont **persistantes** — elles restent disponibles après le redémarrage de l’application. Utilisez le bouton **Clear** au-dessus de la liste des cartes pour supprimer toutes les sessions lorsque vous avez terminé.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect.png" width="320" alt="Inspect tab showing multiple session cards for different devices" />
</div>

### Page Session Details

Appuyez sur une carte de session pour ouvrir sa page de détails complète. La barre supérieure affiche l’adresse de l’appareil et son descripteur, un bouton **reload** pour relancer la reconstruction et un bouton **share** pour exporter et partager un rapport PDF de cette session.

La page de détails comporte trois onglets :

#### Associations

Liste tous les objets de communication lus depuis la mémoire de l’appareil et possédant des adresses de groupe associées :

| Column | Description |
|---|---|
| Number | Index de l’objet de communication |
| Flags | R (Read), W (Write), C (Communication), T (Transmit), U (Update), I (Read-on-Init) |
| Size | Taille de l’objet (1 bit, 1 octet, 2 octets, etc.) |
| Group addresses | Adresses de groupe associées à cet objet |

Chaque adresse de groupe est cliquable. Comme le type de point de données (DPT) n’est pas connu uniquement à partir de la mémoire, un champ de saisie de valeur brute hex ou décimale est proposé pour envoyer des commandes de test.

Les boutons **Export CSV** et **Export TXT** exportent la liste des associations uniquement pour cet appareil.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect-associations.png" width="320" alt="Associations tab showing communication objects with flags, size, and linked group addresses" />
</div>

#### Device Info

Affiche la carte complète des informations appareil (mêmes champs que l’action Read Info de l’onglet Devices). Inclut un bouton **Read Info** si les informations n’ont pas encore été lues, ainsi qu’un bouton **Copy All** qui copie tous les champs dans le presse-papiers afin de les partager avec des collègues.

#### Addresses

Table contenant toutes les adresses de groupe lues depuis la table d’adresses de l’appareil en mémoire, avec des colonnes pour l’index, le format 3 niveaux, le format 2 niveaux et la valeur hex. Chaque ligne peut être copiée individuellement. Les boutons **Copy All** et **Export CSV** sont disponibles au-dessus de la table.

---

## Menu Tune

L’icône tune dans la barre supérieure fournit deux actions d’export pour le résultat du dernier scan de ligne :

- **Export as text** — exporte un rapport TXT contenant l’horodatage du scan, la passerelle utilisée, la zone/ligne scannée, le média et la liste des appareils découverts avec leurs informations
- **Export as PDF** — même contenu au format PDF
