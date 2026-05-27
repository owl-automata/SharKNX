# Formats d'exportation

SharKNX peut exporter des données dans cinq formats en fonction de la source, facilitant ainsi le diagnostic KNX de vos bâtiments intelligents :

| Format | Source | Extension |
|--------|--------|-----------|
| [CSV de télégramme](#telegram-csv) | Monitor, Shark Hunt Monitor | `.csv` |
| [Texte de Line Scan](#line-scan-text) | Scan page → résultats de Line Scan | `.txt` |
| [PDF de Line Scan](#line-scan-pdf) | Scan page → résultats de Line Scan | `.pdf` |
| [PDF des tables du participant](#device-tables-pdf) | Inspect page → tables du participant | `.pdf` |
| [JSON de Shark Hunt](#shark-hunt-json) | Shark Hunts page | `.json` |

Sur mobile, le fichier exporté est proposé via la feuille de partage du système. Sur ordinateur (Windows, macOS), une boîte de dialogue native d'enregistrement de fichier ou de dossier s'ouvre pour sauvegarder les données de votre installation domotique.

---

## CSV de télégramme

Exporté depuis la Monitor page et depuis n'importe quelle Shark Hunt Monitor page en utilisant le export/save button ou le tune menu, un outil idéal pour analyser votre domotique KNX.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-telegram-sheet.png" width="320" alt="Telegram export bottom sheet" />
</div>

### Nom de fichier

```
SharKNX_[Context]_YYYY-MM-DD_HHMMSS.csv
```

`[Context]` est soit `Monitor`, soit le nom du Shark Hunt (nettoyé, max 30 caractères). Exemple : `SharKNX_Monitor_2026-05-16_143022.csv`.

### Structure du fichier

La première ligne est toujours un commentaire d'identification :

```
# SharKNX Export v1
```

Ceci est suivi d'une ligne d'en-tête facultative, puis d'une ligne de données par télégramme.

### Colonnes sélectionnables par l'utilisateur

Ces colonnes sont activées ou désactivées individuellement dans le export bottom sheet avant l'enregistrement de votre diagnostic KNX :

| Colonne | En-tête | Description |
|--------|--------|-------------|
| ID | `ID` | Position séquentielle du télégramme dans la liste |
| Heure | `Time` | Horodatage au format `HH:MM:SS.mm` |
| Source | `Source` | Adresse physique du participant émetteur |
| Destination | `Destination` | Adresse de groupe du télégramme |
| Nom | `Name` | Nom de l'adresse de groupe issu du projet ETS (vide si aucun projet n'est chargé) |
| Type | `Type` | Type APCI : `Write`, `Read`, `Response`, etc. |
| Valeur | `Value` | Valeur décodée issue du projet ETS (vide si aucun projet n'est chargé) |
| Brut | `Raw` | Charge utile brute sous forme de chaîne hex ; toujours présente dans les données du bus |

### Colonnes de métadonnées

Cinq colonnes structurelles sont **toujours ajoutées**, quelle que soit la sélection de l'utilisateur. Elles sont utilisées pour l'importation aller-retour dans SharKNX pour votre installation domotique :

| Colonne | Type | Description |
|--------|------|-------------|
| `_timestampMs` | integer | Horodatage Unix en millisecondes |
| `_isGroupAddress` | boolean | Indique si la destination est une adresse de groupe |
| `_priority` | string | Champ de priorité KNX |
| `_hopCount` | integer | Compteur de sauts (Hop count) de la trame du télégramme |
| `_numericValue` | float | Représentation numérique de la valeur décodée (si disponible) |

### Options

| Option | Par défaut | Description |
|--------|---------|-------------|
| Délimiteur | Virgule | Séparateur de champ : `,`, `;`, ou tabulation |
| Inclure les en-têtes | Activé | Écrit les noms des colonnes comme première ligne de données |
| Max télégrammes | Tous | Limite optionnellement aux N premières lignes |

### Importation

Un fichier CSV SharKNX peut être réimporté dans le Monitor via le tune menu → **Import SharKNX CSV**. Le fichier doit comporter la ligne d'en-tête `# SharKNX Export v1`. L'importation écrase la liste actuelle de télégrammes.

**Fichier d'exemple :** [sample-telegrams.csv](../../../../assets/examples/exports/sample-telegrams.csv)

---

## Texte de Line Scan

Exporté depuis la Scan page après la fin d'un scan de ligne, via le utilities menu → **Export as Text**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-scan-utilities.png" width="320" alt="Scan page utilities menu showing export options" />
</div>

### Nom de fichier

```
line_scan_{area.line}_{YYYY-MM-DD}.txt
```

Exemple : `line_scan_1.1_2026-05-16.txt`.

### Structure du fichier

Le rapport de diagnostic KNX est divisé en trois sections séparées par des lignes en pointillés.

**Bloc d'en-tête**

```
Generated     : 2026-05-16 14:30:22
ETS Project   : My Building
Gateway       : Secure Tunnel  192.168.2.7:3671  (1.1.0)
Line          : 1.1
Medium        : TP
Range         : 0 - 255
Devices Found : 12
Duration      : 38s
```

**Liste des participants** — tableau numéroté compact :

```
  [1]   1.1.1    MDT SCN-00.02        (0x0900)
  [2]   1.1.5    Siemens 5WG1...      (0xFFFF)  [DataSecure]
  ...
```

Chaque ligne affiche pour votre installation domotique : l'index, l'adresse physique, la chaîne de modèle, le descripteur hex, et un indicateur `[DataSecure]` si le descripteur est `0xFFFF`.

**Résultats détaillés** — un bloc par participant, avec quatre sous-sections :

| Sous-section | Champs |
|------------|--------|
| Identité | Descripteur, Rôle du participant, Nom du participant, DataSecure |
| Matériel | N° de série, Fabricant, Info de commande, Version du firmware, Type de matériel, Longueur max APDU |
| Application | État de charge, État d'exécution, Version de l'app, État de charge de la table d'adresses, État de charge de la table d'association, État de charge de la table des objets de groupe |
| Statut | Mode de programmation, Indicateurs d'erreur, Contrôle du participant |

Les champs qui n'ont pas été lus (par exemple, si **Read Info** n'a pas été déclenché pour un participant lors du diagnostic KNX) sont affichés avec `–`.

**Fichier d'exemple :** [sample-line-scan.txt](../../../../assets/examples/exports/sample-line-scan.txt)

---

## PDF de Line Scan

Exporté depuis la Scan page une fois qu'un scan de ligne est terminé, via le utilities menu → **Export as PDF** pour un rapport complet de vos bâtiments intelligents.

### Nom de fichier

```
line_scan_{area.line}_{YYYY-MM-DD}.pdf
```

Exemple : `line_scan_1.1_2026-05-16.pdf`.

### Contenu

Le PDF contient les mêmes informations que le rapport [Texte de Line Scan](#line-scan-text) pour votre diagnostic KNX, formaté comme un document A4 avec le logo SharKNX, des bandes de section et un ombrage de ligne alterné. Les numéros de page et l'horodatage de génération apparaissent dans le pied de page.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-line-scan-pdf.png" width="600" alt="Line scan PDF report preview" />
</div>

**Fichier d'exemple :** [sample-line-scan.pdf](../../../../assets/examples/exports/sample-line-scan.pdf)

---

## PDF des tables du participant

Exporté depuis la Inspect page une fois que les tables du participant ont été lues, via le export button dans la barre supérieure. Un Bulk export est également disponible pour générer un PDF par participant à partir de la session d'inspection en cours, facilitant ainsi la gestion de votre installation domotique.

### Nom de fichier

Un seul participant :

```
device_tables_{individual_address}_{YYYY-MM-DD}.pdf
```

Le **Bulk export** produit plusieurs fichiers avec le même modèle, enregistrés dans un dossier choisi par l'utilisateur (ordinateur) ou partagés sous forme de lot (mobile).

Exemple : `device_tables_1.1.5_2026-05-16.pdf`.

### Sections

| Section | Contenu |
|---------|---------|
| **En-tête + Info** | Adresse physique du participant, horodatage d'exportation, nom du projet ETS (si chargé) |
| **Objets de communication** | Table d'association développée avec des sous-lignes d'adresses de groupe — affiche le numéro de chaque objet de communication, son nom (si disponible depuis ETS), ses indicateurs (flags) et les adresses de groupe liées |
| **Table des adresses de groupe** | Entrées GrAT brutes : index d'emplacement (slot), valeur de l'adresse de groupe |
| **Info du participant** | Champs d'identité, de matériel, d'application et de statut (mêmes champs que le Texte de Line Scan) — présent uniquement si l'action **Read Info** a été effectuée avant l'exportation |

Chaque section commence sur une nouvelle page afin que les rapports multi-sections se paginent proprement pour un suivi optimal de vos bâtiments intelligents.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-device-tables-pdf.png" width="600" alt="Aperçu du rapport PDF des tables du participant" />
</div>

**Fichier d'exemple :** [sample-device-tables.pdf](../../../../assets/examples/exports/sample-device-tables.pdf)

---

## JSON de Shark Hunt

Exporté depuis la **Shark Hunts page** (toutes les chasses) ou depuis le menu d'action d'une chasse individuelle (chasse unique). Le format est le même dans les deux cas — un tableau (array) d'objets de chasse.

### Nom de fichier

L'application propose un nom de fichier au moment de l'exportation. L'extension du fichier est toujours `.json`.

### Structure du fichier

Le fichier JSON est un tableau. Chaque élément représente une définition complète de Shark Hunt, incluant son nom, les actions du moniteur, ainsi que tous les filtres configurés pour le diagnostic KNX et le contrôle KNX de votre installation domotique. Squelette d'exemple :

```json
[
  {
    "name": "HVAC Diagnostics",
    "monitor_actions": [
      {
        "name": "All writes to zone 1",
        "filters": { ... }
      }
    ]
  }
]
```

Un export de chasse unique (single-hunt) enveloppe cette chasse dans le même tableau de premier niveau afin que le format d'importation soit identique, quel que soit le nombre de chasses contenues dans le fichier pour votre gestion domotique KNX.

**Fichier d'exemple :** [sample-shark-hunt.json](../../../../assets/examples/exports/sample-shark-hunt.json)

### Importation

Sur la **Shark Hunts page**, le tune menu → **Import Hunts** accepte un fichier `.json` contenant un ou plusieurs objets de chasse. Les chasses importées sont ajoutées à la fin de la liste existante — elles n'écrasent pas les chasses déjà configurées dans votre système de bâtiments intelligents.
