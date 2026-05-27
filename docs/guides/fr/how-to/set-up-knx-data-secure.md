# Comment configurer KNX Data Secure

KNX Data Secure chiffre les télégrammes KNX individuels au niveau de la couche application. Pour recevoir et envoyer correctement des télégrammes sécurisés, SharKNX a besoin des clés de groupe de votre projet ETS et, pour l'envoi, d'une adresse d'émetteur configurée. Ce guide détaille ces deux étapes pour optimiser votre **installation domotique**.

Pour en savoir plus sur le fonctionnement de KNX Data Secure, consultez la page de concept [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Prérequis

- Un fichier de projet ETS `.knxproj` incluant des adresses de groupe KNX Data Secure.
- Une adresse physique KNX que SharKNX peut utiliser comme identité d'émetteur. Cette adresse doit exister dans le projet ETS et disposer des droits d'accès aux adresses de groupe vers lesquelles vous prévoyez d'envoyer des commandes.

> **Contrainte KNX IP Secure :** L'envoi via KNX Data Secure nécessite que le moniteur fonctionne sur un tunnel KNX IP Secure. Si votre passerelle ne prend pas en charge KNX IP Secure, il existe deux solutions de contournement dans ETS — voir la page de concept [KNX Data Secure](../concepts/knx-data-secure.md#sending-constraints) pour plus de détails.

---

## Partie 1 — Charger les clés de groupe

Les clés de groupe sont intégrées dans le fichier `.knxproj`. Il suffit de charger le projet : SharKNX extrait les clés automatiquement.

1. Allez sur la **Project** page.
2. Appuyez sur le **folder FAB** pour ouvrir le sélecteur de fichiers, ou sélectionnez un projet récemment chargé dans la liste d'historique.
3. Sélectionnez votre fichier `.knxproj`.
   - Si le projet est protégé par un mot de passe, saisissez-le lorsque l'application vous le demande.
4. Une fois le projet chargé, vérifiez la présence du bandeau **Data Secure banner** en haut de la **Project page**. S'il apparaît, cela signifie que le projet contient des adresses de groupe Data Secure et que les clés ont bien été chargées pour le **diagnostic KNX**.

---

## Partie 2 — Configurer l'adresse de l'émetteur

SharKNX doit savoir quelle adresse physique KNX utiliser lors de l'envoi de télégrammes Data Secure. Sans cela, les envois sécurisés échoueront.

1. Depuis la **Project page**, appuyez sur le bandeau **Data Secure banner**. Cela ouvre le volet de configuration de l'émetteur.
   - Alternativement, naviguez dans **Project → onglet Devices**, trouvez le participant dont vous souhaitez utiliser l'adresse comme émetteur, et accédez à la configuration de l'émetteur à partir de là.
2. Dans le volet de configuration de l'émetteur, choisissez l'une des deux approches :

### Option A — Configurer une adresse physique spécifique

1. Appuyez sur **Add sender address**.
2. Saisissez l'adresse physique (par ex. `1.1.250`), ou appuyez sur l'icône de recherche pour sélectionner un participant depuis le projet chargé.
3. Confirmez. L'adresse est enregistrée en tant qu'émetteur de confiance.

### Option B — Utiliser l'adresse d'émetteur globale (automatique)

Si vous préférez ne pas spécifier manuellement chaque adresse individuelle :

1. Appuyez sur **Set global sender address**.
2. Saisissez l'adresse à utiliser pour tous les envois sécurisés.

SharKNX utilisera cette adresse pour toute adresse de groupe Data Secure qui n'a pas d'adresse d'émetteur spécifique configurée.

> Si aucune des deux options ne comporte une adresse figurant dans la liste des émetteurs de confiance du projet ETS pour une adresse de groupe donnée, le participant récepteur rejettera le télégramme. Assurez-vous que l'adresse que vous configurez a bien été ajoutée à la liste des émetteurs de l'objet de groupe dans ETS afin de garantir le **contrôle KNX**.

---

## Partie 3 — Vérification

1. Démarrez le moniteur (connectez-vous à votre passerelle et appuyez sur le bouton d'action flottant FAB de démarrage sur la **Monitor page**).
2. Déclenchez un télégramme Data Secure sur le bus — par exemple, en appuyant sur un interrupteur.
3. Le télégramme doit apparaître dans la liste du moniteur avec sa valeur décodée (et pas seulement brute). Cela confirme que la clé de groupe a été correctement appliquée.
4. Pour vérifier l'envoi : depuis le moniteur, maintenez le doigt appuyé sur une ligne de télégramme d'adresse de groupe Data Secure pour ouvrir le concepteur de commandes (**command composer**) pré-rempli avec son adresse et son DPT. Envoyez une commande d'écriture. Le participant devrait répondre comme prévu au sein de vos **bâtiments intelligents**.

---

## Remarques

- Les clés de groupe sont lues à chaque fois que vous chargez un projet. Si les clés ETS ont été modifiées (par exemple, après une nouvelle mise en service), rechargez le projet pour récupérer les clés mises à jour.
- Les adresses d'émetteur persistent après le redémarrage de l'application. Vous n'avez besoin de les configurer qu'une seule fois par projet.
- Le badge Data Secure sur la **Monitor page** et sur les pages **Shark Hunt** indique l'état actuel de l'émetteur en un coup d'œil — la couleur orange signifie que les émetteurs ne sont pas encore configurés, le vert signifie que tout est prêt.
