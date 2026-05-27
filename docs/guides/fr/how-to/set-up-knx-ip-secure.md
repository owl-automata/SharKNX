# Comment configurer KNX IP Secure

KNX IP Secure chiffre la connexion tunnel entre SharKNX et votre passerelle en utilisant AES-128 CCM sur TCP. Avant que SharKNX puisse se connecter à une passerelle sécurisée, l'application a besoin des identifiants correspondants. Ce guide explique comment les charger au sein de votre **installation domotique**.

Pour en savoir plus sur ce que protège KNX IP Secure et son fonctionnement, consultez la page de concept [KNX IP Secure](../concepts/knx-ip-secure.md).

---

## Ce dont vous avez besoin

L'une des sources d'identifiants suivantes (toutes générées par ETS) :

| Format | Comment l'obtenir |
|---|---|
| Fichier de clés `.knxkeys` | Exporter depuis ETS : Projet → Sécurité → Exporter le fichier de clés (Export keystore) |
| Fichier de projet ETS `.knxproj` | Le même fichier de projet utilisé pour charger les adresses de groupe ; il contient déjà les identifiants des participants |
| Clé de dorsale / Backbone key (chaîne hex) | Se trouve dans ETS sous les paramètres IP Secure de l'interface |

---

## Étape 1 — Ouvrir l'onglet Security

1. Rendez-vous sur la **Discovery** page.
2. Appuyez sur l'onglet **Security** tab.

---

## Étape 2 — Charger les identifiants

Trois méthodes sont disponibles. Utilisez celle qui correspond à ce que vous possédez :

### Méthode A — Charger un fichier de clés `.knxkeys`

1. Appuyez sur **Load .knxkeys file**.
2. Sélectionnez le fichier `.knxkeys` depuis le stockage de votre appareil.
   - Si le fichier est protégé par un mot de passe, saisissez le mot de passe du trousseau (keystore) lorsque l'application vous le demande.
3. Une carte récapitulative apparaît pour confirmer le nombre d'identifiants d'interface chargés.

### Méthode B — Charger les identifiants depuis un fichier de projet ETS

Si vous avez déjà un fichier `.knxproj` chargé ou disponible :

1. Appuyez sur **Load from ETS project**.
2. Sélectionnez le fichier `.knxproj` (ou confirmez le projet déjà chargé).
   - Si le projet est protégé par un mot de passe, saisissez le mot de passe du projet lorsque l'application vous le demande.
3. Les identifiants sont extraits du fichier de projet et chargés automatiquement pour votre **diagnostic KNX**.

### Méthode C — Saisir une clé de dorsale (backbone key) manuellement

1. Appuyez sur **Enter backbone key**.
2. Collez ou saisissez la clé de dorsale hexadécimale à 32 caractères.
3. Confirmez. La clé est enregistrée et sera utilisée pour toute passerelle qui la requiert afin d'assurer le **contrôle KNX**.

---

## Étape 3 — Vérifier la carte de la passerelle

1. Allez sur l'onglet **Discover** tab et scannez les passerelles, ou ouvrez l'onglet **Config** tab si votre passerelle est déjà enregistrée.
2. Localisez votre passerelle sécurisée. Sa carte doit afficher une icône de cadenas (**lock icon**) indiquant que KNX IP Secure est pris en charge.
3. Si les identifiants ont été chargés avec succès, l'icône de cadenas apparaît remplie/active. Si l'icône est vide ou si la carte de la passerelle affiche un avertissement d'identifiant, répétez l'Étape 2 avec le bon fichier.

---

## Étape 4 — Se connecter

1. Appuyez sur **Select** sur la carte de la passerelle pour la définir comme passerelle active.
2. Démarrez le moniteur (ou connectez-vous depuis une page Shark Hunt). SharKNX utilisera automatiquement le tunnel sécurisé TCP.
3. Si la connexion réussit, le badge de connexion devient vert et les télégrammes commencent à défiler normalement, validant le bon fonctionnement au sein de vos **bâtiments intelligents**.

Si la connexion échoue avec une erreur de sécurité, les causes les plus courantes sont :
- Un mauvais fichier de clés keystore (identifiants d'une autre passerelle).
- Un mot de passe de projet ou de keystore incorrect.
- La clé d'outil (tool key) de la passerelle a été modifiée dans ETS après l'exportation du fichier de clés — ré-exportez le fichier de clés depuis ETS et rechargez-le.

---

## Remarques

- Les identifiants chargés via `.knxkeys` ou `.knxproj` sont stockés sur l'appareil et persistent après le redémarrage de l'application. Vous n'avez pas besoin de les recharger à chaque session pour la gestion de votre **domotique KNX**.
- Si un fichier `.knxkeys` contains contient des clés d'outil pour des participants individuels (utilisées pour les opérations de gestion des appareils), celles-ci sont également chargées à cette étape et seront disponibles dans les pages Management et Project.
- Vous pouvez consulter l'historique des fichiers d'identifiants précédemment chargés dans l'onglet **Security** tab.
- Pour utiliser un autre trousseau de clés (keystore), chargez simplement le nouveau fichier — il remplacera les identifiants précédents.
