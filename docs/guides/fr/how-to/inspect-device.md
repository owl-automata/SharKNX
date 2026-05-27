# Comment inspecter les objets de communication d'un participant

L'onglet **Inspect tab** de la **Management page** lit les tables de communication d'un participant directement depuis sa mémoire et reconstitue les objets de communication existants, leurs indicateurs (flags) ainsi que les adresses de groupe qui y sont connectées — le tout sans nécessiter de projet ETS. C'est la méthode la plus fiable pour comprendre un participant inconnu ou mal documenté au sein de votre installation en **domotique KNX**.

---

## Prérequis

- Être connecté à une passerelle KNX (voir [Se connecter à une passerelle](connect-to-gateway.md)).
- L'adresse physique du participant que vous souhaitez inspecter.

---

## Étapes

1. Allez sur la **Management page** → onglet **Inspect tab**.
2. Saisissez l'adresse physique du participant dans le champ de saisie.
   - Vous pouvez également accéder à cet onglet avec le champ pré-rempli depuis l'onglet **Prog. Mode tab** (appuyez sur **Comm. Info** sur une carte), depuis une carte de participant du **Line Scan** (appuyez sur **Rebuild Communication**), ou depuis n'importe quelle fiche détaillée de participant.
3. Appuyez sur **Read**. Une barre de progression affiche l'opération en cours (table des adresses, table des associations, objets de communication).
4. Un badge de session apparaît pour le participant. La couleur de la bordure indique le succès (vert) ou l'échec (rouge).

---

## Lire les informations complètes du participant

La lecture de la table de communication n'inclut pas par défaut les informations détaillées du participant (fabricant, firmware, etc.). Appuyez sur **Read Full Info** sur le badge de session pour récupérer ces détails séparément, ce qui est idéal pour le **diagnostic KNX**.

---

## Visualiser les détails de la session

Appuyez sur le badge de session pour ouvrir sa page de détails complète. La barre supérieure dispose d'un bouton de rafraîchissement (**reload**) pour relancer la lecture, et d'un bouton de partage (**share**) pour exporter et partager un rapport PDF de cette session.

La page de détails comporte trois onglets :

### Associations

Liste tous les objets de communication auxquels au moins une adresse de groupe est connectée :

| Numéro | Flags | Taille | Adresses de groupe |
|---|---|---|---|
| Numéro | Index de l'objet de communication |
| Flags | R Read · W Write · C Communication · T Transmit · U Update · I Read-on-Init |
| Taille | Taille des données de l'objet (1 bit, 1 octet, 2 octets, etc.) |
| Adresses de groupe | Adresses connectées à cet objet |

Appuyez sur n'importe quelle adresse de groupe pour lui envoyer une commande **Read** ou **Write**. Étant donné que le DPT (Type de point de données) ne peut pas être connu uniquement à partir de la mémoire, un champ de saisie de valeur hex/décimale brute est utilisé à la place d'une interface utilisateur adaptée au DPT pour assurer le **contrôle KNX**.

Utilisez **Export CSV** ou **Export TXT** pour exporter la liste des associations de cette session.

### Device Info

Affiche la carte complète des informations du participant si l'action **Read Full Info** a été exécutée. Comprend un bouton **Copy All** pour copier tous les champs dans le presse-papiers.

### Addresses

Un tableau de toutes les adresses de groupe trouvées dans la table des adresses du participant en mémoire (index, 3 niveaux, 2 niveaux, hex). Utilisez **Copy All** ou **Export CSV** pour extraire la liste complète.

---

## Gestion des sessions

Les sessions sont **persistantes** — elles survivent aux redémarrages de l'application et restent disponibles jusqu'à ce que vous les effaciez.

- **Clear** (au-dessus de la liste des badges) — supprime toutes les sessions.
- **Export** (au-dessus de la liste des badges) — exporte toutes les sessions ensemble sous la forme d'un seul document PDF.
- **Share** (barre supérieure de la page de détails d'une session) — exporte et partage uniquement cette session sous forme de PDF.

---

## Remarques

- Un échec de lecture (bordure rouge) signifie généralement que le participant ne répond pas, qu'il est en état d'erreur ou que l'adresse est incorrecte. Utilisez l'option **Check** depuis l'onglet **Devices tab** pour vérifier au préalable que le participant est bien présent sur le bus de vos **bâtiments intelligents**.
- Si le participant nécessite des clés d'outil (Tool keys) KNX Data Secure pour les opérations de gestion de l'appareil, chargez le fichier `.knxkeys` dans la **Discovery page** → onglet **Security tab** avant de lancer la lecture de votre **installation domotique**.
