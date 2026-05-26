# Projets ETS dans SharKNX

SharKNX peut charger un fichier de projet ETS standard (`.knxproj`) pour enrichir chaque partie de l'application avec les noms, les DPT (Types de points de données) et la structure que vous avez déjà définis dans ETS pour votre **installation domotique**. Cette page explique ce que cela signifie en pratique — ce que SharKNX fait avec le fichier, ce qu'il ne fait pas, et ce qu'il faut garder à l'esprit.

---

## Le fichier de projet n'est jamais modifié

Charger un fichier `.knxproj` dans SharKNX est une opération en lecture seule. SharKNX lit le fichier une fois, extrait les données dont il a besoin pour la **domotique KNX**, et les stocke en interne. **Le fichier d'origine sur votre appareil n'est jamais modifié ni écrasé.** Vous n'avez pas à craindre que SharKNX corrompe votre projet, crée des conflits de versions ou cause des problèmes lorsque vous ouvrirez le même projet dans ETS par la suite.

---

## Ce que le chargement d'un projet débloque

Sans projet, SharKNX fonctionne toujours — vous pouvez vous connecter à une passerelle, surveiller le bus et envoyer des commandes en utilisant des adresses de groupe brutes. Tout est fonctionnel mais non nommé. Le chargement d'un projet change considérablement l'expérience de **contrôle KNX** :

**Page Project — quatre vues structurées :**
Les onglets **Group Addresses**, **Devices**, **Topology** et **Buildings** se remplissent avec les données de votre projet, reflétant la structure que vous avez dans ETS pour vos **bâtiments intelligents**. Vous pouvez parcourir l'ensemble de la hiérarchie, rechercher parmi tous les noms et appuyer sur n'importe quelle adresse de groupe pour envoyer directement une commande **Read** ou **Write**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-group-addresses.png" width="320" alt="Page Project montrant l'arborescence des adresses de groupe avec les groupes principaux, les groupes médians et les adresses de groupe d'un projet ETS chargé" />
</div>

**Page Monitor — télégrammes nommés et décodés :**
Les télégrammes entrants sont automatiquement associés au projet chargé. Chaque ligne de télégramme affiche le nom de l'adresse de groupe et une valeur décodée lisible basée sur son DPT, au lieu d'une simple charge utile hexadécimale RAW. Lors d'un **diagnostic KNX**, le composeur de commandes utilise le projet pour pré-remplir le nom de l'adresse de groupe et le DPT lorsque vous appuyez sur une adresse de groupe.

**KNX Data Secure — extraction automatique des clés :**
Si votre projet contient des adresses de groupe KNX Data Secure, leurs clés de groupe sont extraites automatiquement. SharKNX les utilise pour décrypter les télégrammes Data Secure entrants dans le moniteur et pour crypter les commandes Data Secure sortantes. Aucune étape distincte d'importation d'identifiants n'est nécessaire pour la sécurité au niveau du groupe. Voir [KNX Data Secure](knx-data-secure.md) pour plus de détails.

---

## Objets de communication

Lorsque le paramètre **Load communication objects** est activé (par défaut), SharKNX analyse et stocke également les objets de communication pour chaque participant (Device) auquel des adresses de groupe sont connectées. Cela ajoute un niveau de détail supplémentaire :

- Dans l'onglet **Devices**, vous pouvez ouvrir une page dédiée aux objets de communication par participant, affichant tous les objets de comm connectés avec leurs drapeaux (flags), tailles, fonctions et adresses de groupe liées.
- Cela est particulièrement utile pour le **diagnostic KNX** des participants — vous pouvez voir d'un coup d'œil quels objets de comm sont mappés à quelles adresses de groupe et envoyer des commandes de test directement depuis cette vue.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-comm-objects.png" width="320" alt="Page des objets de communication pour un participant montrant le numéro d'objet, les drapeaux, la fonction, la taille et les adresses de groupe liées" />
</div>

Désactiver ce paramètre réduit l'utilisation de la mémoire, ce qui peut être pertinent sur les appareils disposant d'une RAM limitée ou pour de très grands projets. Le reste des données du projet (adresses de groupe, topologie, bâtiments) est toujours chargé normalement.

---

## Ce que SharKNX ne fait pas

SharKNX est un outil de terrain, pas un outil de mise en service. Il y a des choses qu'il ne fait délibérément pas avec le projet ETS :

- **Aucune modification de paramètre.** SharKNX ne peut ni lire ni modifier les paramètres des participants stockés dans le projet. Seul ETS peut écrire des paramètres dans les participants.
- **Aucun téléchargement de programme d'application.** SharKNX ne peut pas programmer ou flasher les participants avec leur logiciel d'application. Cela reste exclusivement du domaine d'ETS.
- **Aucune connexion à un serveur ou une licence ETS.** SharKNX lit directement le fichier `.knxproj` exporté. Il ne se connecte pas à ETS, ne nécessite pas qu'ETS soit en cours d'exécution, et ne consomme pas de licence ETS.

**La programmation des adresses physiques** est la seule opération d'écriture prise en charge par SharKNX qui se rapporte aux données du projet — mais elle écrit directement dans le participant physique sur le bus via la communication de gestion KNX, et non dans le fichier `.knxproj`. Le fichier de projet en lui-même reste inchangé.

---

## Maintenir les données du projet à jour

SharKNX lit le fichier de projet au moment où vous le chargez. Si vous apportez par la suite des modifications dans ETS et exportez un nouveau `.knxproj`, SharKNX ne prendra pas en compte ces modifications automatiquement — vous devez recharger le fichier mis à jour.

La fonction **Apply project data** dans le menu **tune** de la page **Monitor** facilite cela : après avoir chargé un projet mis à jour, vous pouvez appliquer les nouveaux noms et DPT aux télégrammes déjà capturés dans la liste du moniteur, sans avoir à réenregistrer une session.

---

## Formats pris en charge

| Format | Pris en charge |
|---|---|
| `.knxproj` (ETS5) | ✅ |
| `.knxproj` (ETS6) | ✅ |
| Projets protégés par mot de passe | ✅ (mot de passe demandé lors de l'importation) |
| `.knxpkg` ou autres formats ETS | — |

Un seul projet peut être chargé à la fois. Le chargement d'un nouveau projet remplace le projet actuel. Les projets précédemment chargés sont conservés dans une liste d'historique pour un rechargement rapide sans avoir à parcourir de nouveau le système de fichiers.
