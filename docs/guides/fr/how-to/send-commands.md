# Comment envoyer des commandes KNX

SharKNX peut envoyer des commandes de lecture (read) et d'écriture (write) à n'importe quelle adresse de groupe KNX lorsque la surveillance est active. Ce guide présente le concepteur de commandes, tous ses points d'entrée et la manière d'utiliser les badges d'envoi rapide (quick-send chips) pour les commandes répétitives.

---

## Prérequis

- Une passerelle sélectionnée et le moniteur en cours d'exécution (voir [Se connecter à une passerelle](connect-to-gateway.md)).
- Optionnellement, un projet ETS chargé afin que les noms des adresses de groupe et les DPT soient pré-remplis automatiquement.

---

## Le concepteur de commandes (Command Composer)

Le concepteur de commandes est l'interface d'envoi principale. Il comporte quatre champs :

| Champ | Description |
|---|---|
| **Group address** | L'adresse de groupe KNX de destination. Saisissez-la manuellement (par ex. `1/2/3`) ou appuyez sur l'icône de recherche pour parcourir votre projet ETS chargé. |
| **Command type** | **Write** pour envoyer une valeur, **Read** pour demander la valeur actuelle. |
| **DPT** | Type de point de données et sous-type (par ex. DPT 1.001 — Switch). Rempli automatiquement si l'adresse est sélectionnée à partir des données du projet. |
| **Value** | Pour les commandes d'écriture : la valeur à envoyer, présentée sous la forme d'un champ de saisie adapté au DPT (interrupteur, curseur, sélecteur de couleur, champ numérique, etc.). |

Appuyez sur **Send** pour transmettre la commande. Elle apparaît immédiatement dans la liste des télégrammes du moniteur pour assurer le **contrôle KNX**.

---

## Points d'entrée

### Depuis la Monitor Page (Méthode principale)

1. Démarrez le moniteur — le bouton d'action flottant (FAB) vert de démarrage se transforme en un **send FAB** rouge.
2. Appuyez sur le **send FAB**.
3. Un volet inférieur s'ouvre. Appuyez sur **New command** pour ouvrir le concepteur de commandes.
4. Remplissez les champs et appuyez sur **Send**.

### Badges d'envoi rapide (Quick-Send Chips)

Après l'envoi d'une commande, un badge (**chip**) apparaît dans le volet inférieur, affichant l'adresse de groupe et la valeur. Ces badges persistent pendant toute la durée de la session.

- **Appuyez sur un badge** pour renvoyer instantanément la même commande sans rouvrir le concepteur.
- **Maintenez le doigt appuyé sur un badge** pour rouvrir le concepteur de commandes avec l'adresse de groupe et le DPT déjà pré-remplis — utile pour renvoyer la commande avec une valeur différente.

### Depuis un télégramme de la liste du moniteur

1. Appuyez sur n'importe quelle ligne de télégramme pour ouvrir sa fiche détaillée.
2. Appuyez sur **Write** — le concepteur de commandes s'ouvre avec l'adresse de groupe et le DPT pré-remplis à partir du télégramme.
3. Saisissez une valeur et appuyez sur **Send**.

La fiche détaillée dispose également d'un bouton **Read** qui envoie immédiatement une demande de lecture sans ouvrir le concepteur.

### Depuis la Project Page — Onglet Group Addresses

1. Allez sur la **Project** page → onglet **Group Addresses**.
2. Naviguez dans l'arborescence et appuyez sur une adresse de groupe individuelle.
3. Dans le volet inférieur, appuyez sur **Write** pour ouvrir le concepteur de commandes pré-rempli avec l'adresse et le DPT, ou appuyez sur **Read** pour envoyer immédiatement une commande de lecture.

### Depuis la Project Page — Onglet Devices

1. Allez sur la **Project** page → onglet **Devices**.
2. Développez un participant et appuyez sur n'importe quelle adresse de groupe répertoriée sous celui-ci.
3. Le même volet inférieur apparaît — appuyez sur **Write** ou **Read**.

### Depuis la page des objets de communication

1. Allez sur la **Project** page → onglet **Devices**.
2. Appuyez sur un participant (ou maintenez le doigt appuyé sur un participant qui possède des adresses de groupe) pour ouvrir sa fiche détaillée.
3. Appuyez sur **Communication Objects** pour ouvrir la page des objets de communication de ce participant.
4. Appuyez sur n'importe quelle adresse de groupe affichée sous un objet de communication — le même volet inférieur Read/Write apparaît, pré-rempli avec l'adresse et le DPT.

### Depuis l'onglet Inspect — Associations

Lorsque vous avez reconstitué les tables de communication d'un participant dans l'onglet **Management → Inspect**, l'onglet Associations répertorie toutes les adresses de groupe trouvées dans la mémoire du participant.

1. Appuyez sur n'importe quelle adresse de groupe dans l'onglet Associations.
2. Étant donné que le DPT n'est pas disponible uniquement à partir de la mémoire du participant, un **champ de saisie de valeur brute** (raw value) est affiché à la place d'une interface adaptée au DPT. Saisissez une valeur hexadécimale ou décimale et envoyez.
3. Un bouton **Read** est également disponible pour envoyer une demande de lecture à cette adresse.

---

## Envoyer une commande de lecture

Une demande de lecture (read request) demande au participant détenant actuellement l'état d'une adresse de groupe de répondre avec sa valeur actuelle. Le télégramme de réponse apparaîtra dans la liste du moniteur. Si l'application était déjà en cours de surveillance lorsque vous avez appuyé sur **Read** depuis la page Project, elle écoute la réponse de cette adresse pendant environ une seconde et affiche le résultat directement dans le volet inférieur, facilitant ainsi votre **diagnostic KNX**.

---

## Remarques

- L'envoi est possible uniquement lorsque le moniteur est en cours d'exécution. Les cartes d'action dans les Shark Hunts font exception — elles se connectent et envoient indépendamment pour chaque recherche.
- Si vous utilisez une adresse de groupe **KNX Data Secure**, l'adresse de l'émetteur doit être configurée avant que les écritures sécurisées ne soient acceptées par le participant. Consultez le guide [Configuration de KNX Data Secure](setup-knx-data-secure.md).
- Les commandes que vous envoyez apparaissent dans la liste du moniteur comme n'importe quel autre télégramme, ce qui vous permet de voir immédiatement si le bus les a acquittées au sein de votre **installation domotique** pour une gestion optimale de vos **bâtiments intelligents**.
