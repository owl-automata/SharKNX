# Comment charger un projet ETS

Le chargement d'un fichier `.knxproj` permet à SharKNX d'accéder aux noms des adresses de groupe, aux types de points de données (DPT), aux métadonnées des participants et aux clés KNX Data Secure. Sans projet, le moniteur affiche uniquement des valeurs hex brutes sans aucun nom, ce qui limite les capacités de **diagnostic KNX**.

---

## Avant de commencer

Le fichier `.knxproj` doit déjà se trouver sur votre appareil. Si ce n'est pas le cas, transférez-le au préalable :
- Partagez-le depuis ETS directement vers votre téléphone via une application de messagerie, un e-mail ou AirDrop.
- Enregistrez-le sur un espace de stockage cloud (iCloud, Google Drive, OneDrive) et ouvrez-le à partir de là.
- Transférez-le via USB.

SharKNX prend en charge les fichiers `.knxproj` issus d'**ETS5 et ETS6**, y compris les projets protégés par un mot de passe pour la sécurisation de votre **installation domotique**.

---

## Étapes

1. Rendez-vous sur la **Project** page (deuxième onglet de la navigation inférieure).
2. Appuyez sur le **folder FAB**.
   - Si vous avez déjà chargé des projets auparavant, un volet historique (**history sheet**) s'ouvre. Appuyez sur n'importe quelle entrée pour la recharger instantanément — pas besoin de parcourir vos fichiers.
   - Pour charger un nouveau fichier, appuyez sur **Browse** (ou le bouton du sélecteur de fichiers) pour ouvrir le sélecteur de fichiers du système.
3. Sélectionnez votre fichier `.knxproj`.
4. Si le projet est protégé par un mot de passe, saisissez-le lorsque l'application vous le demande et confirmez.
5. Le projet se charge. La barre de recherche, le bouton développer/réduire et les quatre onglets (**Group Addresses**, **Devices**, **Topology**, **Buildings**) deviennent actifs.

---

## Ce qui change après le chargement

- La **Monitor page** et le **Shark Hunt monitor** afficheront désormais les noms des adresses de groupe et les valeurs décodées pour les télégrammes entrants, facilitant ainsi le **contrôle KNX**.
- La barre de recherche de la **Project page** vous permet de filtrer l'ensemble des adresses de groupe, des participants et des éléments du bâtiment par nom.
- Si le projet contient des adresses de groupe configurées en **KNX Data Secure**, un bandeau apparaît sous la barre d'onglets. Appuyez dessus pour configurer les adresses d'émetteur avant d'envoyer des commandes sécurisées. Consultez le guide [Configuration de KNX Data Secure](setup-knx-data-secure.md).

---

## Charger depuis d'autres pages

Vous n'êtes pas obligé de naviguer vers la **Project page** pour charger un projet. Le badge **ETS Project badge** présent sur la **Monitor page** et sur les **Shark Hunt** pages propose un bouton **Load project** lorsqu'aucun projet n'est chargé — un appui dessus ouvre le même volet historique (**history sheet**) et le sélecteur de fichiers.

---

## Mettre à jour ou remplacer un projet

SharKNX ne conserve qu'un seul projet à la fois. Pour passer à un export plus récent ou à un autre projet de votre **domotique KNX** :

1. Appuyez à nouveau sur le **folder FAB** sur la **Project page** (ou sur le badge **ETS Project badge** n'importe où dans l'application).
2. Sélectionnez le fichier `.knxproj` mis à jour.
3. Le nouveau projet remplplace immédiatement le précédent.

> Si le moniteur est actif lorsque vous chargez un nouveau projet, celui-ci s'appliquera aux nouveaux télégrammes entrants. Les télégrammes déjà présents dans la liste conservent les métadonnées du projet précédent jusqu'à ce que la liste soit effacée.

Pour décharger complètement un projet sans en charger un nouveau, appuyez sur l'icône **tune icon** sur la **Project page** et sélectionnez **Unload project**.

---

## Remarques

- Charger un mauvais projet (qui ne correspond pas à votre installation physique) entraînera des noms d'adresses de groupe et des valeurs décodées erronés dans le moniteur. Vérifiez toujours que vous disposez du bon projet pour le site sur lequel vous intervenez, en particulier pour la gestion de **bâtiments intelligents**.
- Le fichier de projet est lu une seule fois au moment du chargement. SharKNX ne reste pas connecté à ETS et ne détecte pas les modifications apportées dans ETS après le chargement du fichier. Rechargez le fichier après toute modification effectuée dans ETS.
- SharKNX ne modifie jamais le fichier `.knxproj`.
