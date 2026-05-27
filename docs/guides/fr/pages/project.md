# Page Project

La page Project est la deuxième page de la barre de navigation inférieure. C’est ici que vous chargez un fichier de projet ETS et parcourez son contenu à travers quatre vues structurées : Group Addresses, Devices, Topology et Buildings.

---

## Chargement d’un projet

Appuyez sur le **folder FAB** pour ouvrir le sélecteur de fichiers et sélectionner un fichier `.knxproj`. Si vous avez déjà chargé des projets auparavant, une fenêtre d’historique apparaît d’abord — sélectionnez une entrée récente ou appuyez sur **Browse** pour choisir un nouveau fichier. Les projets protégés par mot de passe sont pris en charge ; l’application demande le mot de passe pendant l’import.

Le chargement d’un nouveau projet remplace le projet actuellement chargé. Les données du projet précédemment chargé sont supprimées de la mémoire.

> Pour comprendre ce que fait ou ne fait pas le chargement d’un projet, voir [ETS Projects in SharKNX](../concepts/ets-project-in-sharknx.md).

---

## Barre Search and Filter

Une fois un projet chargé, une barre de recherche et de filtre apparaît sous la barre des onglets. Saisissez n’importe quel texte pour rechercher dans tous les noms du projet — adresses de groupe, appareils, bâtiments, lignes et fonctions. Les résultats se mettent à jour au fur et à mesure de la saisie dans l’onglet actuellement actif.

À côté de la barre de recherche se trouve un bouton **Expand All / Collapse All** qui développe ou réduit toutes les sections arborescentes de l’onglet courant en une seule action.

---

## Bannière KNX Data Secure

Si le projet chargé contient des adresses de groupe KNX Data Secure, une bannière apparaît sous la barre des onglets afin de vous inviter à configurer les Data Secure senders. Appuyer sur cette bannière ouvre la page de configuration des Data Secure Senders, où vous définissez quelle adresse physique SharKNX doit utiliser comme expéditeur pour chaque adresse de groupe sécurisée. Cette configuration est nécessaire pour envoyer des commandes Data Secure ; la supervision fonctionne sans cette étape. Voir [KNX Data Secure](../concepts/knx-data-secure.md) pour plus de détails.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-data-secure-banner.png" width="320" alt="Project page with the data secure banner below the tab bar after loading a project with secure group addresses" />
</div>

---

## Onglet Group Addresses

Cet onglet affiche la hiérarchie des adresses de groupe telle qu’elle est configurée dans ETS : groupes principaux au premier niveau, développés en groupes intermédiaires, eux-mêmes développés en adresses de groupe individuelles.

Appuyez sur un groupe principal ou intermédiaire pour le développer ou le réduire. Appuyez sur une **group address** pour ouvrir sa fenêtre d’actions rapides, qui affiche :
- Nom de l’adresse de groupe
- Type de point de données (DPT) et sous-type
- Bouton **Read** — envoie une requête de lecture sur le bus et affiche la réponse directement dans la fenêtre dans un délai d’une seconde si une réponse est reçue
- Bouton **Write** — ouvre le composeur de commande avec l’adresse de groupe et le DPT préremplis ; saisissez une valeur puis envoyez

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-group-addresses.png" width="320" alt="Group Addresses tab showing the main group tree expanded to individual group addresses" />
</div>

> Une passerelle doit être sélectionnée pour envoyer des commandes de lecture ou d’écriture. Si aucune n’est sélectionnée, l’application vous demandera d’en choisir une.

---

## Onglet Devices

Cet onglet liste tous les appareils du projet classés par adresse physique. Les appareils ayant des adresses de groupe associées peuvent être développés pour afficher ces adresses — appuyez sur l’une d’elles pour ouvrir la même fenêtre d’actions rapides que dans l’onglet Group Addresses.

**Appuyez** sur un appareil sans adresses de groupe, ou effectuez un **appui long** sur un appareil avec adresses de groupe, pour ouvrir la **device detail sheet**. Cette fenêtre contient :

### Carte Device Info
Une carte compacte indiquant si l’adresse physique de l’appareil et le programme applicatif sont chargés dans le projet ETS.

### Actions de diagnostic rapides

| Action | Fonction |
|---|---|
| **Check** | Vérifie si l’appareil est présent et répond sur le bus |
| **Read Info** | Lit les informations détaillées directement depuis l’appareil (voir ci-dessous) |
| **Toggle Programming Mode** | Active ou désactive à distance le mode programmation de l’appareil |
| **Program Address** | Recherche un appareil en mode programmation et lui écrit une nouvelle adresse physique |

**Read Info** récupère les informations suivantes depuis l’appareil :
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

### Bouton Communication Objects

Ouvre la page dédiée **Communication Objects page** pour cet appareil (voir ci-dessous).

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-device-detail.png" width="320" alt="Device detail bottom sheet showing the info card, four quick action buttons, and the Communication Objects button" />
</div>

---

## Communication Objects Page

Accessible depuis le bouton Communication Objects dans la fenêtre de détails appareil. Cette page affiche tous les objets de communication de l’appareil connectés à au moins une adresse de groupe.

En haut de la page, les dates **last modified** et **last downloaded from ETS** de l’appareil sont affichées.

Chaque entrée d’objet de communication affiche :
- Numéro de l’objet
- Drapeaux : Read, Write, Communication, Transmit, Update, Read-on-Init
- Nom de fonction (si disponible dans l’application de l’appareil)
- Taille de l’objet (par ex. 1 bit, 1 octet, 2 octets)
- Adresses de groupe connectées — chacune est interactive et ouvre la fenêtre d’actions rapides pour les commandes de lecture/écriture

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-comm-objects.png" width="320" alt="Communication Objects page showing a list of comm objects with flags, size, and linked group addresses" />
</div>

> Le paramètre **Load communication objects** dans Project Settings contrôle si ces données sont analysées lors du chargement du projet. Il est activé par défaut. Le désactiver réduit l’utilisation mémoire pour les grands projets mais supprime l’accès à cette page.

---

## Onglet Topology

Cet onglet affiche la topologie physique du projet : zones au premier niveau, développées en lignes ou segments, puis en appareils. Appuyez sur un appareil pour ouvrir la même fenêtre de détails appareil décrite ci-dessus.

---

## Onglet Buildings

Cet onglet affiche la structure bâtiment telle qu’elle est configurée dans ETS : bâtiments et étages développés en pièces et fonctions, avec les adresses de groupe et appareils associés en dessous. Appuyez sur une adresse de groupe ou un appareil pour ouvrir leurs fenêtres d’actions rapides respectives.

---

## Menu Tune

L’icône tune dans la barre supérieure ouvre une fenêtre inférieure avec une action :

**Unload project** — supprime le projet actuellement chargé de la mémoire. Les quatre onglets reviennent à leur état vide. Les télégrammes capturés dans la page Monitor restent présents mais perdent leurs noms et leurs valeurs décodées.
