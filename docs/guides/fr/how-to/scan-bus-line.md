# Comment scanner une ligne de bus KNX

Un scan de ligne de bus teste chaque adresse physique sur une ligne KNX et répertorie tous les participants qui répondent. Cela vous permet de vérifier ce qui est réellement installé — indépendamment de tout projet ETS — et constitue le moyen le plus rapide d'obtenir une vue d'ensemble d'une installation inconnue lors d'un **diagnostic KNX**.

---

## Prérequis

- Être connecté à une passerelle KNX (voir [Se connecter à une passerelle](connect-to-gateway.md)).
- Connaître la zone KNX et le numéro de ligne à scanner (par ex. zone 1, ligne 1 → `1.1`).

---

## Étapes

1. Allez sur la page **Management** → onglet **Line Scan**.
2. Dans la carte **Scan Settings**, configurez le scan :

   | Paramètre | Description |
   |---|---|
   | **Area / Line** | La zone et la ligne à scanner (par ex. `1.1`). Appuyez sur **Choose from project** pour sélectionner une ligne depuis votre projet ETS chargé — cela définit également le type de média automatiquement. |
   | **Medium type** | TP, IP ou IoT. Doit correspondre au média physique de la ligne. |
   | **Range** | Adresse de début et de fin du participant au sein de la ligne (0–255). Réduisez cette plage pour accélérer le scan ou vérifier un segment spécifique. |

3. Appuyez sur le bouton de balayage **scan FAB** pour démarrer. Le scan peut être arrêté à tout moment.
4. Les participants découverts apparaissent sous forme de cartes. La couleur de la bordure supérieure indique le type de participant :

   | Couleur | Type |
   |---|---|
   | Bleu | Coupleur KNX |
   | Rouge | Participant d'application standard |
   | Vert | Participant KNX Secure |

---

## Lire les informations de participant pour tous les participants découverts

Une fois le scan terminé, appuyez sur **Read Device Info** (au-dessus de la liste des cartes). L'application lit le fabricant, le numéro de série et d'autres détails pour chaque participant découvert, l'un après l'autre.

Ceci est particulièrement utile pour :
- Créer rapidement un inventaire d'une **installation domotique** que vous n'avez pas mise en service vous-même.
- Faire un recoupement avec un projet ETS pour vérifier s'il correspond fidèlement à l'installation physique.
- Identifier les participants ayant des adresses ou des types inattendus sur le bus.

---

## Utilisation des cartes de participant individuelles

Appuyez sur n'importe quelle carte pour ouvrir sa fiche détaillée. À partir de là, vous pouvez :

- **Check** — vérifier si le participant répond toujours et est actif.
- **Read Info** — lire les détails complets du participant (fabricant, firmware, état d'exécution, etc.).
- **Toggle Programming Mode** — activer ou désactiver le mode programmation à distance.
- **Restart** — envoyer une commande de redémarrage au participant.
- **Program Address** — attribuer une nouvelle adresse physique (voir [Programmer l'adresse physique d'un participant](program-device-address.md)).
- **Rebuild Communication** — ouvre l'onglet **Inspect** pré-rempli avec l'adresse de ce participant pour lire ses tables de communication et optimiser le **contrôle KNX**.

---

## Exporter les résultats du scan

Appuyez sur l'icône **tune icon** dans la barre supérieure pour exporter le résultat du scan le plus récent :
- **Export as text** — rapport au format TXT contenant l'horodatage du scan, la passerelle utilisée, la zone/ligne, le média et la liste des participants.
- **Export as PDF** — le même contenu généré au format PDF, idéal pour remettre un rapport propre de vos **bâtiments intelligents**.
