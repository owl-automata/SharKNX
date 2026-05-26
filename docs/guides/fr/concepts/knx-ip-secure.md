# KNX IP Secure

KNX IP Secure est l'extension de sécurité de la couche de transport du protocole KNXnet/IP. Il chiffre la communication entre un participant KNX IP (passerelle ou routeur) et un client tel que SharKNX, empêchant l'écoute clandestine et le **contrôle KNX** non autorisé sur le réseau IP de votre **installation domotique**.

> Cette page explique ce qu'est KNX IP Secure et comment SharKNX le gère. Pour la procédure de configuration étape par étape, voir [Set Up KNX IP Secure](../how-to/setup-knx-ip-secure.md).

---

## Ce que protège KNX IP Secure

Dans une installation KNXnet/IP standard, le trafic de tunneling entre un client et une passerelle transite sous forme de paquets UDP non chiffrés. Quiconque a accès au réseau peut capturer des télégrammes ou injecter des commandes arbitraires. KNX IP Secure résout ce problème en basculant le transport de tunneling sur **TCP** et en appliquant le chiffrement AES-128 CCM à la session, garantissant que :

- Seuls les clients disposant des identifiants corrects peuvent établir une connexion
- Le trafic ne peut pas être lu ou rejoué par d'autres tiers sur le réseau
- La passerelle peut rejeter les tentatives de connexion provenant de sources inconnues

KNX IP Secure fonctionne au niveau de la couche de transport IP. Il ne modifie pas le contenu du télégramme KNX lui-même — c'est le rôle de [KNX Data Secure](knx-data-secure.md).

---

## Deux modes de KNX IP Secure

### Tunneling sécurisé

Le tunneling sécurisé établit une connexion **TCP** chiffrée entre SharKNX et une interface compatible KNX IP Secure (généralement une passerelle KNX IP ou l'interface de tunneling d'un routeur KNX IP), remplaçant le transport UDP utilisé par le tunneling KNXnet/IP standard. Chaque connexion de tunneling possède sa propre adresse physique d'interface et un ensemble correspondant d'identifiants dans le magasin de clés pour la **domotique KNX**.

**Contrainte de l'adresse de l'expéditeur :** Lors d'une connexion via un tunnel KNX IP Secure, l'adresse physique utilisée dans les télégrammes sortants est fixée à l'adresse de l'interface de tunneling attribuée par la passerelle. SharKNX ne peut pas la remplacer. Cela a son importance lorsque vous travaillez avec des adresses de groupe KNX Data Secure, qui valident l'adresse physique de l'expéditeur — voir [KNX Data Secure](knx-data-secure.md) pour plus de détails.

### Multicast sécurisé (Routage IP sécurisé)

Les routeurs KNX IP prenant en charge le routage IP sécurisé utilisent une clé symétrique partagée — la **backbone key** — pour chiffrer le trafic multicast sur le groupe multicast `224.0.23.12` via **UDP**. Tous les participants sur le backbone doivent utiliser la même clé.

SharKNX prend en charge le multicast sécurisé. Lorsqu'un routeur KNX IP est découvert, l'onglet **Discover** affiche à la fois une option multicast standard et une option multicast sécurisée. La sélection de l'option multicast sécurisée nécessite que la backbone key soit chargée.

---

## Fichiers d'identifiants

Les identifiants KNX IP Secure sont distribués via ETS en tant que partie intégrante du magasin de clés du projet pour vos **bâtiments intelligents**. SharKNX accepte les identifiants sous trois formes :

| Format | Ce qu'il contient | Remarques |
|---|---|---|
| `.knxkeys` | Identifiants d'interface, backbone key, clés d'outil | Chiffré avec un mot de passe spécifique au projet défini dans ETS |
| `.knxproj` | Projet ETS complet incluant le magasin de clés intégré | SharKNX extrait les identifiants automatiquement lors de son **diagnostic KNX** |
| Backbone key manuelle | Clé symétrique unique, saisie en hex | Pour le multicast sécurisé uniquement ; à utiliser lorsque vous n'avez que la clé et non le fichier complet du magasin de clés |

**Exportation de `.knxkeys` depuis ETS :** Ouvrez votre projet dans ETS. Depuis l'aperçu du projet (en dehors de l'éditeur de projet), allez dans **More details → Security**, puis choisissez **Backup keyring**. Définissez un mot de passe et enregistrez le fichier.

> **Validation du mot de passe :** SharKNX ne peut pas vérifier si le mot de passe d'un fichier `.knxkeys` est correct au moment de l'importation — c'est une propriété de la spécification KNX. Le mot de passe n'est validé que lors de la tentative de connexion proprement dite. Si la connexion échoue avec une erreur d'authentification, vérifiez que le mot de passe correspond à celui défini lors de l'exportation du magasin de clés dans ETS.

---

## Où charger les identifiants dans SharKNX

Les identifiants peuvent être chargés à trois endroits :

**Onglet Security (page Discovery) :** L'onglet dédié à la gestion de tous les identifiants sécurisés. Appuyez sur le **shield FAB** pour ouvrir la feuille d'importation des identifiants. Après le chargement, l'onglet affiche un aperçu de ce qui a été importé : combien d'interfaces ont été trouvées et combien de participants KNX Data Secure étaient présents dans le fichier. Un bouton d'historique vous permet de recharger rapidement les fichiers récemment utilisés.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-security-tab.png" width="320" alt="Onglet Security affichant un fichier d'identifiants chargé avec le nombre d'interfaces et de participants" />
</div>

**Carte de la passerelle (onglet Discover) :** Si une passerelle découverte annonce une compatibilité KNX IP Secure, sa feuille de détails inclut un bouton **Load Credentials**. Les identifiants chargés ici sont stockés de la même manière que via l'onglet **Security**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-gateway-card.png" width="320" alt="Feuille inférieure de détails de la passerelle avec le bouton Load Credentials pour une passerelle KNX IP Secure" />
</div>

**Menu tune de la page Discovery :** L'icône **tune** dans la barre supérieure de la page **Discovery** offre un accès rapide pour charger des identifiants à partir d'un fichier `.knxkeys` ou `.knxproj` sans avoir à naviguer vers l'onglet **Security**.

Les identifiants sont stockés de manière persistante et restent disponibles après le redémarrage de l'application. Le chargement d'un nouveau fichier remplace les identifiants stockés précédemment.

---

## Clés d'outil KNX Data Secure

Lorsqu'un fichier `.knxkeys` contient des clés d'outil pour les participants KNX Data Secure, SharKNX stocke automatiquement ces clés également. Cela permet des opérations de gestion de participants chiffrées — telles que basculer en mode de programmation, lire les informations du participant, réinitialiser un participant ou lire les tables de communication — sur les participants nécessitant une authentification au niveau de l'outil. Celles-ci sont distinctes des identifiants du tunnel IP Secure et sont utilisées pour la communication au niveau du participant sur le bus KNX TP.

---

## KNX IP Secure vs. KNX Data Secure

| | KNX IP Secure | KNX Data Secure |
|---|---|---|
| **Portée** | Couche de transport IP | Télégramme KNX (couche application) |
| **Ce qu'il chiffre** | Le tunnel UDP/TCP ou le canal multicast | Télégrammes de groupe individuels sur le support KNX |
| **Type d'identifiant** | Identifiants d'interface, backbone key | Clé de groupe par adresse de groupe |
| **Où configuré** | Page **Discovery** → Onglet **Security** | Page **Project** (chargé avec `.knxproj`) |
| **Requis pour** | Se connecter à une passerelle sécurisée | Envoyer/recevoir des télégrammes de groupe sécurisés |

Les deux mécanismes sont indépendants. Une installation peut utiliser KNX IP Secure pour la connexion IP sans KNX Data Secure sur le bus, ou vice versa, ou bien les deux.

Voir [KNX Data Secure](knx-data-secure.md) pour découvrir comment SharKNX gère le chiffrement au niveau du télégramme.
