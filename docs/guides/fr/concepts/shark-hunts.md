# Shark Hunts

Un Shark Hunt (littéralement "Chasse aux requins") est un ensemble d'actions réutilisable et autonome pour tester et diagnostiquer une installation KNX. Au lieu de naviguer vers une adresse de groupe, de sélectionner un point de donnée (DPT) et de composer une commande chaque fois que vous devez effectuer un test, vous créez un hunt une fois et l'exécutez en un seul clic — de n'importe où, à chaque visite sur la même installation.

---

## L'idée principale

Chaque Shark Hunt est stocké sous forme de fichier JSON qui décrit une collection d'**actions d'envoi** (send actions — commandes vers le bus) et d'**actions de surveillance** (monitor actions — sessions de surveillance filtrées). Un hunt peut contenir l'un ou l'autre type, ou les deux. Lorsque vous ouvrez un hunt, toutes ses actions sont présentées sur une seule page sous forme de cartes tactiles, prêtes à être exécutées.

Cela rend les Shark Hunts particulièrement utiles dans plusieurs scénarios :

- **Tests répétés.** La mise en service nécessite souvent l'envoi des mêmes commandes des dizaines de fois au cours de multiples visites sur site. Un hunt capture ces commandes pour que vous n'ayez jamais à les reconstruire manuellement.
- **Délégation de diagnostics.** Un hunt peut inclure tous les détails de connexion pour une installation spécifique. Vous pouvez l'exporter et le partager avec un collègue ou un client qui l'exécutera ensuite sur son propre appareil sans avoir besoin de savoir comment configurer une passerelle ou trouver une adresse de groupe.
- **Séquences de test structurées.** Une action multiple ou séquentielle peut envoyer une série de commandes avec des délais configurables entre elles, couvrant le test d'une scène d'éclairage complète ou un cycle de volet roulant en un seul clic.
- **Filtrage de bus avancé.** Les actions de surveillance peuvent appliquer une logique de filtrage complexe — combinant des plages d'adresses de groupe, des filtres de participants, des filtres de types de télégrammes et des fenêtres de temps — que la barre de filtrage standard du moniteur ne prend pas en charge.

---

## Actions d'envoi (Send Actions)

Trois types d'actions d'envoi sont disponibles :

**Send Fixed** exécute une commande d'écriture (write) ou de lecture (read) unique vers une adresse de groupe spécifique avec une valeur fixe à chaque fois. Utile pour les déclenchements rapides de participants — allumer une lumière, enregistrer une scène, vérifier la valeur d'un capteur.

**Send Multiple / Sequence** exécute une série de commandes fixes dans l'ordre. Chaque commande de la séquence peut avoir un délai configurable avant le déclenchement de la suivante (jusqu'à 10 secondes par étape). Utilisez ceci pour tester les enregistrements de scènes, les séquences de course de volets ou toute logique d'automatisation à plusieurs étapes.

**Send Variable** envoie une valeur que vous choisissez au moment de l'exécution à une ou plusieurs adresses de groupe partageant le même type de point de données (DPT). Lorsque vous appuyez sur la carte de l'action, une feuille de saisie de valeur s'ouvre avec les contrôles DPT appropriés (curseurs, sélecteurs de couleurs, champs numériques, etc.). Utile lorsque vous souhaitez avoir la flexibilité de tester différentes valeurs sans avoir à modifier le hunt.

---

## Actions de surveillance (Monitor Actions)

Trois types d'actions de surveillance sont disponibles :

**Custom Monitor** applique un filtre à conditions multiples au moniteur de bus. Les conditions peuvent filtrer par adresse de groupe (y compris les caractères génériques comme `1/*/0`), par adresse physique de l'expéditeur (y compris les caractères génériques comme `1.*.*`), par type de télégramme (lecture, écriture, réponse), par nom ou texte de description, et par fenêtre de temps. Les conditions sont connectées avec une logique ET/OU (AND/OR), permettant des filtres qui ne peuvent pas être exprimés via la barre de recherche standard du moniteur. Les entrées d'adresses et de participants peuvent également être définies pour exclure plutôt qu'inclure, afin que vous puissiez tout surveiller à l'exception d'une plage spécifique.

**Monitor Space** utilise la structure de bâtiment de votre projet ETS pour définir la cible du filtre. Vous sélectionnez une pièce ou un espace dans la hiérarchie du bâtiment et le moniteur n'affiche que les adresses de groupe ou les participants appartenant à cet espace. Aucune saisie manuelle d'adresse n'est nécessaire.

**Monitor Device** cible un ou plusieurs participants spécifiques de votre projet ETS et surveille toutes les adresses de groupe qui y sont connectées. Efficace pour isoler la communication d'un seul actionneur ou capteur pendant les tests de votre installation KNX.

Lorsque vous ouvrez une action de surveillance dans un hunt, les filtres sont appliqués immédiatement. Un badge dans la vue du moniteur affiche les détails du filtre actif, et une feuille de commutation rapide vous permet de basculer entre toutes les actions de surveillance du hunt sans quitter la page du moniteur.

---

## Partage et portabilité

Les Shark Hunts sont conçus pour être partagés. Chaque hunt peut éventuellement inclure une **passerelle préconfigurée** (preconfigured gateway) — l'adresse IP, le port et les paramètres de connexion pour l'installation pour laquelle il a été conçu. Lorsque quelqu'un ouvre un hunt partagé, cette passerelle apparaît comme une option de connexion afin qu'il puisse se connecter et exécuter le hunt sans avoir besoin de découvrir ou de configurer quoi que ce soit lui-même.

Vous pouvez exporter un seul hunt ou tous vos hunts en même temps sous forme de fichier JSON, puis le partager via n'importe quelle méthode de transfert de fichiers — applications de messagerie, e-mail, disques cloud. L'importation d'un fichier JSON ajoute les hunts qu'il contient à votre liste sans écraser ceux qui existent déjà.

Les cartes de hunt sont codées par couleur afin que vous puissiez voir d'un coup d'œil ce que fait un hunt :

| Couleur de la bordure | Contenu |
|---|---|
| Vert | Actions d'envoi uniquement |
| Bleu | Actions de surveillance uniquement |
| Rouge | À la fois des actions d'envoi et de surveillance |

---

## Persistance

Les hunts sont enregistrés sur l'appareil et persistent après le redémarrage de l'application. Les horodatages de création et de dernière modification de chaque hunt sont stockés et visibles dans la feuille d'informations du hunt.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-main-page.png" width="320" alt="Page principale de Shark Hunts montrant les cartes de hunt avec des bordures codées par couleur" /></td>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Une page Shark Hunt ouverte montrant les cartes d'actions d'envoi et d'actions de surveillance" /></td>
    </tr>
  </table>
</div>

---

## Lectures complémentaires

- [Create a Shark Hunt](../how-to/create-shark-hunt.md) — guide étape par étape pour créer votre premier hunt
