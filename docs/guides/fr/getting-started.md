# Démarrer avec SharKNX

SharKNX est un compagnon de terrain professionnel pour la domotique KNX sur mobile et bureau. Ce guide vous accompagne à travers le flux de travail principal : la connexion à une passerelle KNX IP, le chargement d'un projet ETS et le démarrage d'une session de moniteur de bus en direct pour le diagnostic KNX.

## Prérequis

- Un appareil fonctionnant sous Android, iOS, Windows ou macOS 13+
- Une passerelle KNX IP accessible sur le même réseau IP que votre appareil
- (Recommandé) Un fichier de projet ETS (`.knxproj`) pour votre installation domotique

> **Abonnement :** SharKNX nécessite un abonnement actif. Sans abonnement ni période d'essai actif, vous pouvez uniquement charger un projet ETS y vous ne pourrez pas vous connecter aux passerelles (gateways) ou en multicast. Les forfaits mensuels et annuels incluent un essai gratuit de 14 jours. Un forfait à vie est également disponible sous forme d'achat unique. Voir [Subscription Plans](reference/subscription-plans.md) pour plus de détails.

---

## Étape 1 - Découvrir votre passerelle

La page **Discovery** s'ouvre automatiquement au démarrage de l'application. Il s'agit de la page la plus à gauche dans la barre de navigation inférieure.

1. Appuyez sur le **scan FAB** en bas de la page.  
   L'application envoie des requêtes de recherche KNX IP sur votre réseau local. Toutes les passerelles KNX IP qui répondent apparaissent sous forme de cartes dans la liste pour faciliter votre contrôle KNX.

2. Appuyez sur **Select** sur la carte de la passerelle que vous souhaitez utiliser.  
   La passerelle est déplacée vers la section **Last Selected Gateway** en haut de la page et est mémorisée entre les redémarrages - pas besoin de scanner à nouveau lors de la session suivante.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-discovery.png" width="320" alt="Onglet Discovery montrant la carte d'une passerelle découverte avec les boutons Select et Save" />
</div>

> **Aucune passerelle trouvée ?** Vérifiez que votre appareil se trouve sur le même segment de réseau que la passerelle. En Wi-Fi avec un VLAN filaire, les paquets multicast peuvent être ignorés par le routeur. Utilisez l'onglet **Config** pour ajouter la passerelle manuellement par adresse IP et port, ou activez **Force unicast subnet scan** dans Discover Settings.

> **KNX IP Secure ?** Si votre passerelle nécessite des identifiants KNX IP Secure, appuyez sur la carte de la passerelle et utilisez le bouton **Load Credentials**. Voir [Set Up KNX IP Secure](how-to/setup-knx-ip-secure.md) pour la procédure complète.

> **Sauvegarder pour plus tard :** Appuyez sur **Save** sur la carte d'une passerelle pour l'enregistrer de manière permanente dans l'onglet **Config**. Les passerelles sauvegardées sont disponibles sans avoir besoin de relancer le scan, ce qui est très pratique lorsque vous intervenez à nouveau sur la même installation domotique.

---

## Étape 2 - Charger votre projet ETS

Un projet ETS fournit à SharKNX les noms d'adresse de groupe, les DPT (Type de point de données) et les métadonnées des participants de votre installation. Sans lui, les télégrammes apparaissent sous forme de valeurs hexadécimales RAW sans noms ni valeurs décodées.

1. Appuyez sur la page **Project** (deuxième onglet de la barre de navigation inférieure).
2. Appuyez sur le **folder FAB** pour ouvrir le sélecteur de fichiers. Naviguez jusqu'à votre fichier `.knxproj` et sélectionnez-le.  
   Si vous avez déjà chargé des projets auparavant, un historique s'affiche en premier - sélectionnez une entrée récente ou appuyez sur **Browse** pour choisir un nouveau fichier.
3. Attendez que le chargement du projet se termine. Les quatre onglets (Group Addresses, Devices, Topology, Buildings) se remplissent avec les données de votre projet pour vos bâtiments intelligents.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-load-project.png" width="320" alt="Page Project avec l'arborescence des adresses de groupe développée après le chargement d'un projet ETS" />
</div>

> **Transférer le fichier sur votre appareil :** Exportez votre projet ETS depuis votre PC (`File → Export project` ou clic droit sur le projet dans ETS). Ensuite, transférez le fichier `.knxproj` vers votre mobile en utilisant la méthode qui vous convient - envoyez-le à vous-même via une application de messagerie (par exemple, sauvegardez-le dans votre propre discussion sur Viber, WhatsApp ou Telegram), joignez-le à un e-mail, uploadez-le sur un cloud (Google Drive, iCloud, OneDrive) et ouvrez-le sur votre téléphone, ou copiez-le via USB.

> **Les projets protégés par mot de passe** sont pris en charge. L'application vous demandera le mot de passe du projet lors de l'importation.

> **Ignorer cette étape :** Vous pouvez surveiller le bus sans projet. Les télégrammes n'afficheront que les adresses source et de destination brutes avec les charges utiles en hexadécimal.

---

## Étape 3 - Démarrer le moniteur de bus

1. Appuyez sur la page **Monitor** (quatrième onglet de la barre de navigation inférieure).
2. Appuyez sur le **start FAB** vert.
   - Si aucune passerelle n'est encore sélectionnée, un sélecteur apparaît listant vos passerelles découvertes et sauvegardées - sélectionnez-en une pour continuer.
   - L'application se connecte à la passerelle et commence à recevoir les télégrammes.
3. Les télégrammes entrants apparaissent sous forme de lignes dans la liste. Chaque ligne affiche :
   - Adresse physique de l'émetteur → adresse de groupe de destination
   - Nom de l'adresse de groupe et valeur décodée *(nécessite un projet ETS)*
   - Charge utile hexadécimale RAW
   - Horodatage au format `HH:MM:SS.ms`

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-monitor-active.png" width="320" alt="Page Monitor avec les télégrammes en direct dans la vue en liste" />
</div>

> Appuyez sur la ligne de n'importe quel télégramme pour ouvrir ses détails, y compris la source, la destination, la valeur décodée, ainsi que des boutons pour envoyer une commande **Read** ou **Write** immédiate à cette adresse.

> **Garder l'écran allumé :** Le moniteur s'arrête si l'écran se verrouille sur un appareil mobile. Le mode de maintien de l'écran allumé est activé par défaut dans Monitor Settings pour éviter cela.

---

## Étape 4 - Envoyer une commande

Avec le moniteur en cours d'exécution, vous pouvez envoyer des commandes de test pour votre diagnostic KNX sans quitter la vue du moniteur.

1. Appuyez sur le **send FAB** rouge (il remplace le start FAB une fois que le moniteur est actif).
2. Appuyez sur **New Command** dans la feuille inférieure.
3. Dans le composeur de commandes :
   - Saisissez une adresse de groupe, ou appuyez sur le **search icon** pour parcourir les adresses de groupe de votre projet chargé.
   - Choisissez **Write** ou **Read**.
   - Sélectionnez le DPT (Type de point de données) et le sous-type.
   - Pour une écriture, saisissez la valeur à envoyer.
4. Appuyez sur **Send**. La commande est transmise sur le bus et apparaît immédiatement dans la liste des télégrammes.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-send-command.png" width="320" alt="Page du composeur de commandes montrant la saisie de l'adresse de groupe, le sélecteur DPT et le champ de valeur" />
</div>

> **Renvoi rapide :** Après avoir envoyé une commande, une pastille (chip) avec son adresse et sa valeur apparaît près du **send FAB**. Appuyez sur cette pastille pour renvoyer la commande immédiatement, ou faites un appui long dessus pour rouvrir le composeur avec les champs pré-remplis.

---

## Et ensuite ?

Vous avez maintenant une session de moniteur en direct, un projet ETS chargé contenant vos noms, et vous savez comment envoyer des commandes de test. À partir de là :

| Objectif | Guide |
|---|---|
| Parcourir les adresses de groupe et envoyer des commandes depuis l'arborescence du projet | [Project Page](pages/project.md) |
| Créer des ensembles de commandes et de filtres réutilisables | [Shark Hunts](concepts/shark-hunts.md) |
| Configurer le décryptage des adresses de groupe KNX Data Secure | [Set Up KNX Data Secure](how-to/setup-knx-data-secure.md) |
| Scanner une ligne de bus et vérifier la présence des participants | [Scan Bus Line](how-to/scan-bus-line.md) |
| Exporter votre session de moniteur en CSV ou PDF | [Export Formats](reference/export-format.md) |
| Lire les infos de firmware d'un participant ou basculer en mode de programmation | [Inspect Device](how-to/inspect-device.md) |
