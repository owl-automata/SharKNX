# Page Monitor

La page Monitor fournit une session de supervision KNX en direct. Les télégrammes entrants sont capturés en temps réel et affichés sous forme de liste défilante. Vous pouvez filtrer, inspecter, tracer et exporter les télégrammes, ainsi qu’envoyer des commandes sur le bus sans quitter la page.

---

## Démarrage et arrêt

Appuyez sur le **start FAB** vert pour démarrer une session de supervision.

- Si aucune passerelle n’est sélectionnée, un sélecteur apparaît avec vos passerelles découvertes et enregistrées. Sélectionnez-en une pour continuer.
- L’application se connecte à la passerelle et commence immédiatement à capturer les télégrammes.
- Le FAB devient un **send FAB** rouge pendant l’exécution du monitor (voir [Sending Commands](#sending-commands)).

Appuyez sur le badge **Start/Stop** dans la rangée de badges (voir ci-dessous) pour arrêter le monitor. La liste des télégrammes reste visible après l’arrêt — elle n’est pas effacée tant que vous ne la videz pas explicitement.

---

## Rangée Filter Bar

La rangée de filtres est épinglée au-dessus de la liste des télégrammes et reste toujours visible.

**Text filter bar** — saisissez n’importe quel texte pour filtrer la liste visible des télégrammes. La recherche correspond aux noms d’adresses de groupe, aux valeurs et aux adresses physiques. La liste sous-jacente n’est pas modifiée ; effacez le filtre pour revoir tous les télégrammes capturés.

**Search filter icon** — ouvre une fenêtre inférieure avec deux onglets : l’un listant toutes les adresses de groupe de votre projet ETS chargé, l’autre listant tous les appareils. Appuyez sur une entrée pour l’appliquer immédiatement comme filtre actif. Très utile pour isoler rapidement une adresse de groupe ou un appareil spécifique sans saisie manuelle.

**Always-on-top button** — lorsqu’il est activé (par défaut), la liste défile automatiquement vers le télégramme le plus récent à chaque nouvelle réception. L’affichage détecte automatiquement lorsque vous faites défiler manuellement la liste et suspend l’auto-défilement jusqu’à votre retour en haut. Appuyer sur le bouton lorsqu’il est désactivé replace immédiatement la vue en haut.

**Export button** — ouvre la fenêtre inférieure d’export. Voir [Exporting Telegrams](#exporting-telegrams).

---

## Rangée de badges

Une rangée défilante de badges est épinglée sous la barre de filtres. Chaque badge est interactif.

### Start / Stop
Démarre ou arrête la session de supervision. Même fonction que le start FAB avant le démarrage du monitor.

### Clear
Efface tous les télégrammes de la liste. La session de supervision continue de fonctionner si elle est active.

### ETS Project
Indique si un projet ETS est chargé. Un appui ouvre une fenêtre avec les détails du projet (nom, format des adresses de groupe, dates de création et de modification) ainsi qu’un bouton permettant de décharger le projet. Si aucun projet n’est chargé, la fenêtre contient un bouton **Load Project** ouvrant le même sélecteur de fichiers que la page Project.

### Data Secure
Reflète l’état de KNX Data Secure pour la session actuelle :

| Badge state | Meaning |
|---|---|
| Gray | Aucune adresse de groupe Data Secure dans le projet chargé |
| Amber | Des adresses Data Secure sont présentes, mais les expéditeurs ne sont pas configurés |
| Green | Des adresses Data Secure sont présentes et les expéditeurs sont configurés |

Un appui sur un badge orange ouvre une fenêtre contenant un bouton permettant de naviguer vers la page de configuration des Data Secure Senders. Voir [KNX Data Secure](../concepts/knx-data-secure.md).

### Telegrams
Affiche le nombre actuel de télégrammes. Un appui ouvre une fenêtre contenant :
- **Clear filter** — supprime tout filtre texte ou filtre de recherche actif (affiché uniquement lorsqu’un filtre est actif)
- **Clear telegrams** — efface tous les télégrammes capturés
- **Statistics** — ouvre une vue statistique affichant :
  - Nombre total de télégrammes
  - Taux de télégrammes/seconde (calculé entre le premier et le dernier horodatage)
  - Principales adresses de groupe par pourcentage du total
  - Principales adresses physiques émettrices par pourcentage
  - Principaux types de télégrammes (write, read, response, etc.) par pourcentage

### View
Ouvre les options d’affichage de la liste des télégrammes :
- **Sort order** — plus récents en premier (par défaut) ou plus anciens en premier
- **Address level format** — définit la manière dont les adresses de groupe sont affichées (3 niveaux, 2 niveaux ou libre). Par défaut, utilise le format du projet ETS chargé. Les modifications affectent uniquement les nouveaux télégrammes entrants, pas ceux déjà affichés.
- **View Group** — ouvre une seconde fenêtre permettant de filtrer la liste visible par adresse de groupe, adresse physique, type de télégramme ou priorité. La sélection d’une entrée affiche uniquement les télégrammes correspondants.

### Gateway
Affiche l’adresse IP de la passerelle sélectionnée. La couleur indique l’état de la connexion :

| Colour | State |
|---|---|
| Gray | Aucune passerelle sélectionnée |
| Blue | Passerelle sélectionnée, non connectée |
| Green | Sélectionnée et connectée |

Un appui ouvre une fenêtre avec les détails de la passerelle et un bouton **Clear selection** (disponible uniquement lorsque le monitor est arrêté).

---

## Liste des télégrammes

Chaque ligne de la liste affiche :
- **Adresse physique source → adresse de groupe destination**
- **Nom de l’adresse de groupe** *(nécessite un projet ETS)* | **valeur décodée** *(nécessite un projet ETS)* | **payload hex brut**
- **Horodatage** au format `HH:MM:SS.ms`

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-active.png" width="320" alt="Monitor page with live telegrams in the list view" />
</div>

### Telegram Detail Sheet

Appuyez sur une ligne pour ouvrir la fenêtre de détails du télégramme. Elle affiche :

- Horodatage
- Adresse physique source
- Adresse de groupe destination
- Nom de l’adresse de groupe *(si un projet ETS est chargé)*
- Valeur décodée *(si un projet ETS est chargé)*
- Payload hex brut

Deux boutons d’action sont disponibles :
- **Read** — envoie immédiatement une commande de lecture vers l’adresse de groupe du télégramme
- **Write** — ouvre le composeur de commande avec l’adresse de groupe et le type de point de données préremplis ; saisissez une valeur puis envoyez

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-telegram-detail.png" width="320" alt="Telegram detail sheet showing time, source, destination, value, and Read/Write/Plot buttons" />
</div>

### Plot

Un bouton **Plot** dans la fenêtre de détails ouvre une vue graphique à deux onglets pour l’adresse de groupe sélectionnée :

- **Value tab** — graphique temporel de toutes les valeurs capturées pour cette adresse. Pincez pour zoomer, déplacez horizontalement et appuyez sur un point pour afficher sa valeur exacte et son horodatage.
- **Sources tab** — histogramme des adresses physiques émettrices ayant transmis cette adresse de groupe, utile pour identifier des émetteurs inattendus ou diagnostiquer du « bruit » sur le bus.

Une carte d’informations affiche la plage temporelle couverte par les données du graphique.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-plot.png" width="320" alt="Plot view showing a time series chart of a group address value over time" />
</div>

---

## Sending Commands

Pendant l’exécution du monitor, le FAB devient un **send FAB** rouge. Un appui ouvre une fenêtre inférieure contenant :

- **New Command** — ouvre le composeur de commande. Saisissez une adresse de groupe (ou recherchez-la depuis le projet ETS chargé), sélectionnez write ou read, choisissez le type et le sous-type de point de données, saisissez une valeur puis appuyez sur **Send**. La commande envoyée apparaît immédiatement dans la liste des télégrammes.
- **Quick command chips** — des chips correspondant aux commandes récemment envoyées apparaissent sous le bouton de nouvelle commande. Appuyez sur une chip pour renvoyer instantanément la même commande. Effectuez un appui long sur une chip pour rouvrir le composeur avec les champs préremplis afin de modifier la valeur avant envoi.

---

## Exporting Telegrams

La fenêtre inférieure d’export (ouverte depuis le bouton d’export de la rangée de filtres ou depuis le menu tune) permet d’enregistrer ou partager la liste actuelle des télégrammes sous forme de fichier CSV.

Options disponibles :

| Option | Description |
|---|---|
| Filename | Modifiable, prérempli avec un horodatage |
| Columns | Cases à cocher pour id, time, source, destination, name, type, value, raw |
| Telegram count | Choisissez combien de télégrammes exporter (par ex. les 100 derniers sur 5000) |
| Include headers | Active ou désactive la ligne d’en-tête des colonnes dans le CSV |
| Delimiter | Virgule (par défaut), tabulation ou point-virgule |

**Save** écrit le fichier dans le stockage de votre appareil. **Share** ouvre la fenêtre de partage système afin de l’envoyer directement vers une application de messagerie, un stockage cloud ou un email.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-export.png" width="320" alt="Export bottom sheet showing filename input, column selection tick boxes, and Save/Share buttons" />
</div>

Voir [Export Formats](../reference/export-format.md) pour la structure complète du fichier CSV.

---

## Menu Tune

L’icône tune dans la barre supérieure ouvre des actions supplémentaires pour la page Monitor :

**Import SharKNX CSV** — charge dans la liste des télégrammes un fichier CSV précédemment exporté depuis SharKNX. Les télégrammes importés remplacent la liste actuelle. Le fichier doit correspondre au format d’export SharKNX.

**Export telegrams** — identique au bouton d’export dans la rangée de filtres.

**Import from ETS XML** — charge un fichier d’export de télégrammes provenant du logiciel ETS. Utile pour visualiser et analyser sur mobile un enregistrement réalisé dans ETS ou le partager avec des collègues. Remplace la liste actuelle des télégrammes.

**Apply project data** — après chargement ou mise à jour d’un projet ETS, applique rétroactivement les noms d’adresses de groupe et les types de points de données du projet à tous les télégrammes actuellement présents dans la liste. Le monitor doit être arrêté avant l’exécution de cette opération. Utilisez cette fonction lorsque vous chargez un projet après avoir déjà capturé des télégrammes, ou lorsque vous rechargez un projet mis à jour et souhaitez refléter les nouveaux noms dans les données déjà capturées.
