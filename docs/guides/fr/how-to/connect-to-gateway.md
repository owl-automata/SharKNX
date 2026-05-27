# Comment se connecter à une passerelle KNX

SharKNX se connecte à votre **installation domotique** via une passerelle KNXnet/IP sur le réseau local. Ce guide explique comment découvrir une passerelle automatiquement, l'enregistrer pour une réutilisation rapide, en ajouter une manuellement et établir la connexion pour le **contrôle KNX**.

---

## Option A — Scanner et se connecter (Recommandé pour la première utilisation)

1. Allez sur la **Discovery** page et ouvrez l'onglet **Discover** tab.
2. Appuyez sur le **scan FAB** (icône de radar). L'application envoie des requêtes de découverte KNXnet/IP sur le réseau local et affiche la liste des passerelles qui répondent.
3. Localisez votre passerelle dans les résultats. Chaque carte affiche le nom de la passerelle, l'adresse IP, le port et indique si le protocole KNX IP Secure est pris en charge.
4. Appuyez sur **Select** sur la carte de la passerelle pour la définir comme passerelle active pour la session en cours.
   - Pour l'enregistrer pour les sessions futures, appuyez sur **Save** sur la carte. Les passerelles enregistrées apparaissent dans l'onglet **Config** tab et peuvent être sélectionnées sans avoir à relancer un scan.
5. Naviguez vers la **Monitor** page (ou toute page nécessitant une connexion) et appuyez sur le **connect/start FAB**. SharKNX se connecte automatiquement à la passerelle sélectionnée pour lancer le **diagnostic KNX** au sein de vos **bâtiments intelligents**.

> **Last Selected Gateway :** La dernière passerelle utilisée est mémorisée et s'affiche en haut de la fenêtre contextuelle de connexion sur la **Monitor** page et les **Shark Hunt** pages. Cela signifie que vous n'avez généralement plus besoin de revenir sur la **Discovery** page après la configuration initiale.

---

## Option B — Ajouter une passerelle manuellement

Utilisez cette option lorsque la passerelle se trouve sur un sous-réseau différent ou n'est pas détectable via multicast (par exemple, lors d'un accès à distance via un VPN).

1. Allez sur la **Discovery** page et ouvrez l'onglet **Config** tab.
2. Appuyez sur le **+ FAB** pour ouvrir le formulaire de saisie manuelle de la passerelle.
3. Remplissez les champs requis :

   | Field | Description |
   |---|---|
   | **Name** | Un libellé pour identifier cette passerelle dans la liste |
   | **IP address** | L'adresse IPv4 de la passerelle |
   | **Port** | La valeur par défaut est `3671` |
   | **Use KNX IP Secure** | À activer si la passerelle nécessite un tunnel sécurisé (Tunneling) |
   | **NAT mode** | À activer en cas de connexion via un routeur NAT ou un pare-feu |

4. Appuyez sur **Save**. La passerelle apparaît dans la liste de l'onglet **Config** tab et devient immédiatement disponible pour la sélection.
5. Appuyez sur l'entrée de la passerelle pour la sélectionner, puis démarrez le moniteur ou connectez-vous depuis une page de recherche (hunt page).

> L'onglet **Config** tab prend en charge jusqu'à **50** passerelles enregistrées.

---

## Option C — Connexion via Multicast (Routage IP KNX)

Si votre installation utilise un routeur IP KNX en mode routage, SharKNX peut recevoir et envoyer des données sur le groupe multicast plutôt que de passer par un tunnel (Tunneling) dédié vers une passerelle spécifique.

1. Allez sur la **Discovery** page → onglet **Discover** tab.
2. Si aucun routeur prenant en charge le routage n'est détecté lors du scan, la section multicast peut ne pas s'afficher par défaut. Activez l'option **Always show multicast options** dans **Settings → Discover** pour la rendre visible en permanence.
3. Appuyez sur **Select** sur l'option multicast. Aucune configuration d'adresse IP ou de port n'est nécessaire — l'application utilise l'adresse multicast et le port configurés dans **Settings → Discover** (valeurs par défaut : `224.0.23.12`, port `3671`).

---

## Connexion avec KNX IP Secure

Si la passerelle requiert le protocole KNX IP Secure, chargez vos identifiants dans l'onglet **Security** tab de la **Discovery** page avant de vous connecter. Consultez le guide [Configuration de KNX IP Secure](setup-knx-ip-secure.md).

---

## Dépannage

| Symptôme | Cause probable |
|---|---|
| Aucune passerelle trouvée après le scan | L'appareil et la passerelle se trouvent sur des sous-réseaux différents, ou le trafic multicast est bloqué — essayez l'option **Force unicast subnet scan** dans **Settings → Discover**, ou ajoutez la passerelle manuellement |
| Délai d'attente de la connexion dépassé (Timeout) | L'adresse IP ou le port de la passerelle est incorrect, ou la passerelle est occupée par un autre client (la plupart des passerelles ne prennent en charge qu'un tunnel à la fois) |
| Échec de la connexion sécurisée | Les identifiants ne sont pas chargés, ou le magasin de clés (Keystore) est incorrect — retournez sur l'onglet **Security** tab |
| Passerelle trouvée mais impossible à sélectionner | La passerelle peut exiger le protocole KNX IP Secure et vos identifiants n'ont pas encore été chargés |
