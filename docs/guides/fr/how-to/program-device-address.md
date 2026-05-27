# Comment programmer l'adresse physique d'un participant

SharKNX peut programmer (écrire) l'adresse physique KNX d'un participant directement depuis votre téléphone ou votre PC — sans avoir besoin d'ETS ou d'un accès physique à un ordinateur portable sur site. Deux méthodes sont disponibles : via le bouton de programmation physique, ou via le numéro de série du participant (aucune pression sur le bouton n'est requise). C'est un outil idéal pour optimiser le déploiement de votre **installation domotique**.

---

## Prérequis

- Être connecté à une passerelle KNX (voir [Se connecter à une passerelle](connect-to-gateway.md)).
- La nouvelle adresse physique que vous souhaitez attribuer, soit connue à partir de votre projet, soit saisie manuellement.

---

## Méthode A — Via le bouton de programmation

Utilisez cette méthode lorsque vous avez un accès physique au participant (ou qu'un collègue sur site peut appuyer sur le bouton).

1. Allez sur la page **Management** → onglet **Line Scan**.
2. Lancez un scan de ligne sur la zone/ligne concernée (voir [Scanner une ligne de bus](scan-bus-line.md)), puis appuyez sur la carte du participant que vous souhaitez reprogrammer pour ouvrir sa fiche détaillée.
   - Vous pouvez également aller sur l'onglet **Devices** de la page **Management**, saisir l'adresse physique actuelle du participant et utiliser les actions à partir de là.
3. Dans la fiche détaillée du participant, appuyez sur **Program Address**.
4. Saisissez la nouvelle adresse physique dans le champ de saisie, ou appuyez sur l'icône **search icon** pour en sélectionner une depuis votre projet ETS chargé.
5. Appuyez sur **Program via programming button**.
6. L'application attend jusqu'à **20 secondes** qu'un participant entre en mode programmation. Appuyez sur le bouton de programmation du participant physique pendant ce laps de temps.
7. Lorsque l'application détecte un participant en mode programmation, elle écrit la nouvelle adresse et confirme le succès de l'opération pour assurer un **contrôle KNX** immédiat.

> L'application vérifie si la nouvelle adresse est déjà utilisée par un autre participant sur l'installation réelle. Si un conflit est détecté, vous êtes averti avant la validation de l'écriture.

---

## Méthode B — Via le numéro de série

Utilisez cette méthode lorsque vous disposez déjà du numéro de série du participant grâce à une opération **Read Info** précédente. Aucune pression physique sur le bouton n'est nécessaire — une solution parfaite pour les participants situés dans des endroits difficiles d'accès au sein de vos **bâtiments intelligents**.

1. Assurez-vous d'abord que le numéro de série du participant est connu : effectuez un **Read Info** depuis la carte du participant dans le Line Scan ou depuis l'onglet Devices si ce n'est pas déjà fait.
2. Dans la fiche détaillée du participant ou dans l'onglet Devices, appuyez sur **Program Address**.
3. Saisissez la nouvelle adresse physique ou sélectionnez-la depuis le projet.
4. Appuyez sur **Program via serial number**.
5. L'application s'adresse directement au participant en utilisant son numéro de série et écrit la nouvelle adresse sans nécessiter le bouton de programmation.

---

## Astuce — Basculement à distance du mode programmation

Si vous ne pouvez pas atteindre physiquement le bouton de programmation, utilisez l'option **Toggle Programming Mode** depuis la carte du participant ou l'onglet Devices pour l'activer d'abord à distance. Exécutez ensuite immédiatement **Program via programming button** — l'application le détectera dans la fenêtre de 20 secondes. Désactivez-le à nouveau par la suite. Cette fonction s'avère très pratique lors d'une session de **diagnostic KNX**.

---

## Remarques

- Après la programmation, vérifiez le résultat en appuyant sur **Check** sur la carte du participant pour confirmer que la nouvelle adresse est bien active sur le bus.
- Ce flux de travail prend en charge le processus de mise en service initial : scanner la ligne → identifier tous les participants → programmer les adresses → se connecter et télécharger les programmes depuis ETS.
