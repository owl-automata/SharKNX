# Page Shark Hunts

La page Shark Hunts est l’endroit où vous créez, gérez et exécutez des **shark hunts** — des ensembles réutilisables d’actions d’envoi KNX et de filtres de supervision enregistrés sous forme de fichiers JSON portables. Un hunt fournit une page dédiée avec des actions en un seul tap, des filtres préconfigurés et une passerelle optionnelle intégrée, prête à être partagée avec des collègues ou des clients.

Pour le concept sous-jacent, voir [Shark Hunts](../concepts/shark-hunts.md).

---

## Structure principale de la page

Sous la barre supérieure se trouve une barre de filtre texte. Saisissez du texte pour filtrer les cartes de hunts par nom. L’icône **star** à droite de cette barre permet de filtrer instantanément pour n’afficher que les hunts marqués comme favoris.

La barre supérieure contient :

- **Bouton Help** — ouvre une page de référence dans l’application couvrant le concept de Shark Hunt, les types d’actions et des exemples
- **Icône Tune** — deux actions :
  - **Export Hunts** — exporte tous les hunts existants dans un seul fichier JSON
  - **Import Hunts** — importe un fichier JSON contenant un ou plusieurs hunts

### Création d’un hunt

Appuyez sur le **+ FAB** pour ouvrir l’assistant de création en cinq étapes. Voir [Create a Shark Hunt](../how-to/create-shark-hunt.md) pour un guide complet.

### Cartes de hunts

Chaque hunt créé apparaît sous forme de carte. La couleur de la bordure supérieure indique son type :

| Border colour | Hunt type |
|---|---|
| Green | Actions d’envoi uniquement |
| Blue | Actions de supervision uniquement |
| Red | Actions d’envoi et de supervision |

Chaque carte affiche le nom du hunt, sa description (si disponible) et son type. Elle contient également :

- **Icône étoile** — ajouter ou retirer des favoris
- **Menu trois points** — Edit, Export (JSON unique), Share, Delete et Info
  - **Info** ouvre une fenêtre affichant le nom, le type, le statut favori, le nombre et les noms des actions, ainsi que les horodatages de création et modification

Un appui long sur une carte active le mode multi-sélection, permettant de copier, exporter ou supprimer plusieurs hunts simultanément.

Les cartes de hunts sont persistantes et survivent aux redémarrages de l’application.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-main.png" width="320" alt="Shark Hunts main page showing hunt cards with colour-coded top borders and filter row" />
</div>

---

## Page de détail d’un hunt

Appuyer sur une carte de hunt ouvre sa page dédiée. La barre supérieure affiche un bouton retour et un champ de filtre permettant de rechercher dans les cartes d’actions de cette page.

### Rangée de badges

| Badge | Description |
|---|---|
| **Hunt name** | Un appui ouvre la fenêtre d’informations du hunt (nom, type, favori, nombre d’actions, timestamps) |
| **Connection status** | Rouge = déconnecté, Vert = connecté. Un appui connecte ou déconnecte la passerelle |
| **ETS Project** | Indique si un projet ETS est chargé. Un appui ouvre une fenêtre avec les détails du projet (nom, format des adresses de groupe, dates) et un bouton pour charger ou décharger le projet |
| **Data Secure** | Indique l’état des senders KNX Data Secure. Gris = aucune adresse de groupe Data Secure chargée ; orange = adresses présentes mais senders non configurés (appui pour configurer) ; vert = senders configurés (appui pour consulter) |
| **Gateway** | Affiche l’adresse IP de la passerelle. Bleu = sélectionnée, gris = aucune sélection, vert = sélectionnée et connectée. Un appui ouvre une fenêtre avec les détails et un bouton de suppression de sélection (si non en monitoring) |

### Connexion

Appuyez sur le **FAB vert (connect)** pour vous connecter à la passerelle configurée. Si aucune passerelle n’est sélectionnée, une fenêtre propose les options disponibles — incluant toute passerelle intégrée au hunt lors de sa création, ainsi que les passerelles découvertes et configurées manuellement. Une fois connecté, le FAB devient rouge (stop) pour déconnecter.

Toutes les cartes d’actions sont grisées et non interactives tant que la connexion n’est pas établie.

---

## Section Send Actions

Les cartes d’actions d’envoi sont regroupées dans la partie supérieure de la page du hunt. Un appui exécute immédiatement l’action :

- **Action fixe** — envoie la valeur préconfigurée sans interaction
- **Action multiple / séquence** — envoie toutes les commandes en séquence, avec les délais configurés
- **Action variable** — ouvre une fenêtre inférieure avec une interface adaptée au DPT (par ex. sliders RGB pour couleur, slider pour pourcentage DPT 5.001). Validation via le bouton send

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Hunt detail page showing send action cards in the upper section and monitor action cards below" />
</div>

---

## Section Monitor Actions

Les cartes d’actions de supervision sont regroupées sous les actions d’envoi. Un appui ouvre le **Shark Hunt Monitor** pour cette action — une session de monitoring avec les filtres de l’action appliqués immédiatement.

### Shark Hunt Monitor

La page Shark Hunt Monitor est similaire à la page principale [Monitor](monitor.md) mais limitée au filtre de l’action active. La barre supérieure affiche le nom du hunt en titre et le nom de l’action en sous-titre, ainsi qu’un bouton **save/export** (actif lorsqu’il y a des télégrammes).

#### Rangée de badges

| Badge | Description |
|---|---|
| **Send** | Ouvre une fenêtre de composition de commande. Affiche aussi des chips de commandes récentes ; appui long pour rouvrir le composeur avec les champs préremplis |
| **Filter details** | Affiche les conditions du filtre actif |
| **Clear** | Efface tous les télégrammes |
| **Data Secure** | Identique au badge Data Secure de la page du hunt |
| **View** | Tri et format d’adresses de groupe. Affecte uniquement les nouveaux télégrammes |
| **Statistics** | Nombre total de télégrammes, taux télégrammes/seconde, top adresses de groupe, top émetteurs et types de télégrammes |
| **Gateway** | Identique au badge gateway de la page du hunt |

Le **monitor FAB** fonctionne ainsi :
- FAB principal — vert/start pour démarrer, rouge/stop pour arrêter
- Petit FAB au-dessus — ouvre une liste des actions de monitoring du hunt pour changer de filtre sans quitter la page (action active marquée par un point vert)

#### Liste des télégrammes

Chaque ligne affiche :
- Adresse physique source → adresse de groupe destination
- Nom de l’adresse de groupe | valeur | payload hex brut (nom et valeur nécessitent un projet ETS chargé)
- Horodatage au format HH:MM:SS.ms

Un appui ouvre la fenêtre de détail du télégramme avec tous les champs (temps, source, destination, nom, valeur, payload brut) et deux actions — **Read** (lecture sur le bus) et **Write** (composeur prérempli). Un troisième bouton **Plot** ouvre une vue graphique avec série temporelle et histogramme des sources.

---

## Export

La fenêtre d’export permet de nommer le fichier (prérempli avec un timestamp), choisir les colonnes (ID, time, source, destination, name, type, value, raw), définir le nombre de télégrammes à exporter, activer ou non les en-têtes et choisir le séparateur (virgule, tabulation ou point-virgule).
