# Comment créer un Shark Hunt

Un Shark Hunt est un ensemble réutilisable d'actions d'envoi et de filtres de surveillance enregistré sous forme de fichier portable. Ce guide vous accompagne à travers l'assistant de création en cinq étapes et explique comment configurer chacun des six types d'actions disponibles pour optimiser votre **installation domotique**.

Pour un aperçu global de ce que sont les Shark Hunts et du fonctionnement de la page dédiée, consultez la section [Shark Hunts](../concepts/shark-hunts.md).

> L'application prend en charge jusqu'à **25 hunts**. Chaque hunt prend en charge jusqu'à **25 actions**.

---

## L'assistant de création

Sur la page principale **Shark Hunts**, appuyez sur le **+ FAB** pour ouvrir l'assistant.

Chaque étape de l'assistant dispose de :
- Un **X button** (en haut à gauche) pour fermer — l'application vous avertit en cas de modifications non enregistrées.
- Boutons **Back / Next** en bas pour naviguer entre les étapes.
- Un **Save button** (en haut à droite) qui apparaît dès que vous effectuez une modification, vous permettant de sauvegarder votre progression et de quitter pour terminer plus tard.

---

### Étape 1 — Name and Description

Saisissez un **name** pour le hunt (obligatoire) et une **description** facultative. Activez l'option **Mark as favourite** si vous souhaitez que ce hunt apparaisse en premier lorsque vous filtrez par étoile sur la page principale.

---

### Étape 2 — ETS Project

Choisissez si ce hunt utilisera un projet ETS :

| Option | Quand l'utiliser |
|---|---|
| **Use loaded ETS project** | Un projet est déjà chargé — le hunt utilisera ses adresses de groupe, ses participants et sa structure de bâtiment pour la création d'actions et les filtres de surveillance. |
| **Load a project** | Aucun projet n'est encore chargé — ouvre le sélecteur de fichiers pour que vous puissiez en charger un maintenant. |
| **Manual input** | Vous n'avez pas ou n'avez pas besoin de projet — les adresses de groupe devront être saisies manuellement lors de la création des actions. |

> Les types d'actions **Monitor Space** et **Monitor Device** nécessitent un projet ETS. Si vous ignorez la sélection du projet ici, ces deux types d'actions ne seront pas disponibles à l'Étape 3.

---

### Étape 3 — Actions

C'est ici que vous construisez le contenu du hunt. Appuyez sur **Add action** et choisissez un type d'action dans la liste. Voir la section [Action Types](#action-types) ci-dessous pour tous les détails sur chaque type.

Les actions créées apparaissent sous forme de cartes. Chaque carte dispose des options suivantes :
- **Edit** — rouvrir la configuration de l'action.
- **Copy** — dupliquer l'action (utile pour des actions similaires avec de petites différences).
- **Delete** — supprimer l'action.

Répétez l'opération jusqu'à ce que vous ayez toutes les actions nécessaires.

---

### Étape 4 — Gateway (Facultatif)

Vous pouvez éventuellement intégrer une configuration de passerelle dans le hunt. Cela permet au destinataire d'un hunt partagé de se connecter sans avoir à découvrir ou configurer la passerelle lui-même — idéal pour le partage avec des utilisateurs non experts dans le cadre d'un **diagnostic KNX** à distance.

Sélectionnez l'une des passerelles déjà découvertes ou appuyez sur **Configure manually** pour saisir une adresse IP et un port. Cette étape peut être ignorée si aucune passerelle intégrée n'est nécessaire.

---

### Étape 5 — Review and Create

Un résumé de toutes vos sélections. Vérifiez-les et appuyez sur **Create** pour terminer. Le hunt apparaît sur la page principale sous forme de carte.

---

## Action Types

Chaque page de création d'action nécessite un **action name** (obligatoire) et une **description** facultative. Le **tick FAB** devient actif dès que tous les champs obligatoires sont remplis, et un appui dessus enregistre et crée l'action.

---

### Send Fixed

Envoie une valeur fixe unique à une adresse de groupe chaque fois que l'action est activée pour le **contrôle KNX**.

1. Saisissez l'adresse de groupe, ou appuyez sur le **search icon** pour en sélectionner une depuis le projet ETS chargé (remplit automatiquement le DPT).
2. Choisissez **Write** ou **Read**.
3. Sélectionnez le type et le sous-type de **DPT** (Type de point de données).
4. Pour **Write** : saisissez la valeur à envoyer (par ex. `On`, `75%`, `21.5°C`, `Scene 3`).
5. Appuyez sur le **tick FAB** pour enregistrer.

**Exemples :** Inverser l'état d'une lumière, définir une consigne de thermostat, rappeler une scène, tester la position d'un volet roulant.

---

### Send Multiple / Sequence

Envoie une liste de commandes fixes en séquence, éventuellement avec des temporisations entre elles.

1. Appuyez sur le **+ button** pour ajouter la première commande — le concepteur de commande s'ouvre. Saisissez l'adresse de groupe, le DPT, **Read**/**Write**, et la valeur, puis appuyez sur le **tick FAB** pour l'ajouter.
2. Appuyez à nouveau sur **+** pour ajouter d'autres commandes (jusqu'à **15**).
3. Chaque commande apparaît sous forme de carte extensible affichant le DPT et la valeur.
4. Pour ajouter une temporisation avant une commande : appuyez sur le sous-titre **"Immediate"** sur une carte et saisissez un délai en secondes (max **10 s**). La commande suivante attendra ce délai avant de s'exécuter.
5. Pour réorganiser : appuyez sur la **six-dot drag handle** de n'importe quelle carte et glissez-la vers la position souhaitée.
6. Appuyez sur le **tick FAB** pour enregistrer l'action.

**Exemple :** Définir la scène → attendre 2 s → lire l'état → attendre 1 s → envoyer la confirmation.

---

### Send Variable

Envoie une valeur que vous choisissez au moment de l'exécution à une ou plusieurs adresses de groupe. Utile lorsque vous devez tester différentes valeurs sur la même adresse ou diffuser vers plusieurs adresses liées à la fois dans votre **domotique KNX**.

1. Saisissez une adresse de groupe dans le champ de saisie et appuyez sur **Add**. Répétez l'opération pour chaque adresse cible (jusqu'à **15**).
   - Utilisez le **project search** pour sélectionner plusieurs adresses de groupe à la fois depuis le projet ETS chargé.
2. Toutes les adresses ajoutées doivent partager le même DPT. Les incohérences sont mises en évidence sur les cartes d'adresses mais ne bloquent pas la création — gardez simplement à l'esprit que le participant peut ne pas répondre comme prévu.
3. Appuyez sur le **tick FAB** pour enregistrer.

Lorsque vous lancez cette action sur la page du hunt, un volet inférieur s'ouvre avec un champ de saisie adapté au DPT. Saisissez la valeur et confirmez pour l'envoyer à toutes les adresses cibles.

**Exemples :** Sélectionner toutes les adresses de groupe de consigne de thermostat d'un étage et envoyer 21 °C en un seul geste pour vérifier que chaque zone CVC répond correctement. Ou cibler toutes les adresses de canaux de variateur d'une pièce et faire défiler les valeurs de luminosité pour identifier celle qui provoque un clignotement.

---

### Custom Monitor

Crée un filtre avancé pour une session de surveillance en utilisant une ou plusieurs conditions combinées avec une logique **AND** / **OR**.

1. Appuyez sur le **+ button** pour ajouter une condition. Jusqu'à **10 conditions** peuvent être ajoutées.
2. Choisissez le type de condition :

   | Condition | Ce qu'elle filtre |
   |---|---|
   | **Group address** | Affiche uniquement les télégrammes vers/depuis des adresses de groupe spécifiques. Saisissez les adresses manuellement ou sélectionnez-les depuis le projet. Prend en charge les caractères génériques (`1/*/*`, `1/*/0`). Activez l'option **Exclude** pour inverser (tout afficher sauf ces adresses). |
   | **Device address** | Affiche uniquement les télégrammes provenant d'adresses physiques spécifiques. Saisissez-les manuellement ou utilisez le **project search**. Prend en charge les caractères génériques (`1.*.*`). Activez l'option **Exclude** pour inverser. |
   | **Telegram type** | Filtre par type APCI : **Write**, **Read**, **Response**, ou toute combinaison. |
   | **Text search** | Affiche uniquement les télégrammes dont le nom ou la description de l'adresse de groupe contient une chaîne de recherche. Nécessite un projet ETS chargé. |
   | **Timestamp** | Affiche les télégrammes avant, après ou entre des heures spécifiques. Utile pour tester les automatismes basés sur le temps. |

3. Après avoir ajouté les conditions, définissez l'opérateur logique entre elles : **AND** (toutes les conditions doivent correspondre) ou **OR** (au moins une condition doit correspondre).
4. Appuyez sur le **tick FAB** pour enregistrer.

**Exemples :**
- *Isoler un participant suspect :* Ajoutez une condition **Device address** pour l'émetteur suspecté ET une condition **Group address** pour la plage d'adresses de groupe affectée. Seuls les télégrammes de ce participant vers ces adresses s'afficheront — tout le reste est filtré.
- *Vérifier une automatisation matinale :* Ajoutez une condition **Timestamp** (après 07:00) ET une condition **Telegram type** (**Write** uniquement). Lancez le moniteur le lendemain matin et confirmez que le programmateur a déclenché les bonnes commandes au bon moment.
- *Surveiller tout sauf votre propre trafic de test :* Ajoutez une condition **Device address** avec l'option **Exclude** pour l'adresse physique de votre ordinateur portable ou de votre téléphone, afin que seul le trafic réel de l'installation s'affiche pendant vos tests.

---

### Monitor Space

Crée rapidement un filtre de surveillance limité à un espace physique dans la structure de bâtiment de votre projet ETS. Nécessite un projet ETS (défini à l'Étape 2).

1. Choisissez ce que vous souhaitez surveiller :
   - **Group addresses** — surveiller toutes les adresses de groupe attribuées aux participants de l'espace sélectionné.
   - **Device senders** — surveiller toutes les adresses physiques des participants situés dans l'espace sélectionné.
2. Appuyez sur **Select space** — la structure de votre bâtiment ETS apparaît sous forme de volet. Sélectionnez un étage, une pièce ou n'importe quel emplacement (par ex. `Kitchen`, `Living Room`).
3. Appuyez sur le **tick FAB** pour enregistrer.

> Jusqu'à **750 adresses** peuvent être capturées à partir d'une seule sélection d'espace. Les grands espaces contenant de nombreux participants peuvent approcher de cette limite.

---

### Monitor Device

Crée un filtre de surveillance limité à un ou plusieurs participants spécifiques de votre projet ETS. Nécessite un projet ETS (défini à l'Étape 2).

1. Appuyez sur **Select devices** — la liste des participants de votre projet apparaît. Sélectionnez un ou plusieurs participants.
2. Le filtre surveillera toutes les adresses de groupe connectées aux participants sélectionnés.
3. Appuyez sur le **tick FAB** pour enregistrer.

> La même limite de **750 adresses** s'applique. Utile pour tester la communication entre deux participants ou pour vérifier toutes les sorties d'un contrôleur au sein de vos **bâtiments intelligents**.

---

## Modifier un Hunt existant

Depuis la page principale, appuyez sur le **three-dot menu** de n'importe quelle carte de hunt et sélectionnez **Edit**. Cela réouvre l'assistant avec toutes les données existantes. Vous pouvez modifier le nom, ajouter ou supprimer des actions, changer de passerelle ou mettre à jour tout autre paramètre.

---

## Partager un Hunt

Depuis le **three-dot menu**, appuyez sur **Share** pour envoyer le hunt sous forme de fichier JSON via n'importe quelle cible de partage (e-mail, application de messagerie, stockage cloud). Le destinataire pourra l'importer via l'option **tune icon → Import Hunts** sur sa propre page **Shark Hunts**. Un seul fichier exporté peut contenir un ou plusieurs hunts.
