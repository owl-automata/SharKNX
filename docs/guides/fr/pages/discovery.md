# Page Discovery

La page Discovery est la première page de la barre de navigation inférieure et s’ouvre par défaut au démarrage de l’application. C’est ici que vous pouvez rechercher, configurer et gérer les passerelles KNX IP auxquelles vous connecter pour vos projets de domotique KNX, de bâtiments intelligents et de diagnostic KNX. Elle comporte trois onglets : **Discover**, **Config** et **Security**.

---

## Onglet Discover

Appuyez sur le **scan FAB** pour commencer la recherche de périphériques KNX IP sur le réseau local. L’application envoie des requêtes de recherche KNX IP et affiche sous forme de cartes tous les appareils qui répondent.

### Cartes de passerelle

Chaque carte de passerelle découverte affiche :
- Nom de la passerelle (tel qu’annoncé par l’appareil)
- Adresse IP et port de tunneling

Deux boutons sont disponibles sur chaque carte :

**Select** — définit cette passerelle comme cible de connexion active. La passerelle est déplacée vers la section **Last Selected Gateway** en haut de la page et reste mémorisée après le redémarrage de l’application. La sélection d’une passerelle ne lance pas immédiatement la connexion ; l’application se connecte automatiquement lorsqu’une action est effectuée (démarrage du moniteur, envoi d’une commande, etc.).

**Save** — enregistre la passerelle dans l’onglet **Config** afin de pouvoir la réutiliser sans nouvelle découverte. Utile lorsque vous intervenez régulièrement sur la même installation domotique.

Un appui sur une carte (et non sur un bouton) ouvre la **gateway detail sheet** :
- Adresse physique KNX
- Numéro de série
- Adresse MAC
- Type de média
- Capacités de gestion de l’appareil (si prises en charge)
- Bouton **Connect** — établit immédiatement la connexion ; utile pour tester l’accessibilité, bien que cela ne soit pas nécessaire en fonctionnement normal
- Bouton **Load Credentials** *(passerelles KNX IP Secure uniquement)* — charge les identifiants `.knxkeys` ou `.knxproj` pour cette passerelle. Voir [KNX IP Secure](../concepts/knx-ip-secure.md).

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-scan.png" width="320" alt="Discover tab showing discovered gateway cards with Select and Save buttons" /></td>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-gateway-detail.png" width="320" alt="Gateway detail bottom sheet showing address, serial number, MAC, and Connect button" /></td>
    </tr>
  </table>
</div>

### Last Selected Gateway

Si une passerelle a déjà été sélectionnée, elle apparaît dans une section épinglée en haut de l’onglet Discover. Elle est automatiquement re-sélectionnée au redémarrage de l’application afin de pouvoir reprendre rapidement vos opérations de contrôle KNX sans relancer un scan réseau.

### Section Multicast

Si un routeur KNX IP avec capacités de routage IP est découvert, une section **Multicast** apparaît sous la liste des cartes. En l’ouvrant, deux options sont disponibles :
- **Multicast** — multicast KNX IP standard sur `224.0.23.12:3671`
- **Secure Multicast** — multicast chiffré nécessitant une clé backbone (voir [KNX IP Secure](../concepts/knx-ip-secure.md))

Sélectionnez l’une de ces options pour l’utiliser comme type de connexion à la place d’un tunnel unicast.

---

## Onglet Config

L’onglet Config stocke les passerelles enregistrées manuellement ou via le bouton **Save** de l’onglet Discover. Les passerelles présentes ici sont accessibles à tout moment sans avoir besoin de relancer une découverte.

### Ajouter une passerelle manuellement

Appuyez sur le **"+" FAB** pour ouvrir la page de configuration manuelle de passerelle. Renseignez les champs suivants :

| Field | Description |
|---|---|
| Friendly name | Libellé affiché sur la carte afin d’identifier cette passerelle |
| IP address / hostname | Adresse IP de la passerelle ou nom d’hôte DNS (par exemple un domaine DynDNS) |
| KNX individual address | Adresse physique KNX de la passerelle ; valeur par défaut `15.15.255`. Doit correspondre à l’appareil pour les connexions KNX IP Secure. |
| Port | Port de tunneling ; valeur par défaut `3671` |
| Use NAT | À activer dans les scénarios VPN où le client et la passerelle se trouvent sur des sous-réseaux différents |
| KNX IP Secure | Marque cette connexion comme connexion KNX IP Secure |

Appuyez sur **Save** pour créer l’entrée. La passerelle apparaît ensuite sous forme de carte dans l’onglet Config.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-config-manual.png" width="320" alt="Manual gateway configuration page with fields for name, IP, port, and secure options" />
</div>

### Cartes de passerelle Config

Les cartes de l’onglet Config fonctionnent de manière identique à celles de l’onglet Discover (Select, Save, detail sheet) avec un ajout : un bouton **Edit** permettant de rouvrir la page de configuration afin de corriger ou mettre à jour n’importe quel champ sans supprimer puis recréer l’entrée.

L’onglet Config peut contenir jusqu’à 50 passerelles enregistrées.

---

## Onglet Security

L’onglet Security permet de charger les identifiants KNX IP Secure et KNX Data Secure utilisés dans toute l’application pour les opérations de diagnostic KNX et de gestion sécurisée des installations domotiques.

Appuyez sur le **shield FAB** pour ouvrir la fenêtre d’importation des identifiants. Trois méthodes d’entrée sont disponibles :

| Method | Use case |
|---|---|
| `.knxkeys` file | Exporté depuis ETS. Contient les identifiants d’interface, la clé backbone et les clés d’outil. Nécessite le mot de passe du trousseau défini lors de l’export. |
| `.knxproj` file | Export complet de projet ETS. SharKNX extrait automatiquement tous les identifiants sécurisés. |
| Manual backbone key | Permet de saisir directement une clé backbone multicast en hex. Utilisé uniquement pour le multicast sécurisé. |

Après chargement, l’onglet affiche un résumé :
- Nombre d’interfaces KNX IP trouvées dans le fichier
- Nombre d’appareils KNX Data Secure présents (par adresse physique)

Un bouton **History** en haut permet de recharger rapidement les fichiers d’identifiants récemment utilisés sans avoir à parcourir de nouveau le système de fichiers.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-security-tab.png" width="320" alt="Security tab showing a loaded credential file summary with interface and device counts" />
</div>

> **Clés d’outil :** Un fichier `.knxkeys` peut également contenir des clés d’outil pour les appareils KNX Data Secure. Si elles sont présentes, SharKNX les stocke automatiquement afin d’autoriser les opérations chiffrées de gestion des appareils (activation du mode programmation, lecture des informations appareil, etc.). Voir [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Menu Tune

L’icône tune dans la barre supérieure ouvre une fenêtre inférieure offrant un accès rapide au chargement des identifiants sans naviguer vers l’onglet Security :

- **Load credentials from .knxkeys** — ouvre le sélecteur de fichiers pour un fichier `.knxkeys`
- **Load credentials from .knxproj** — ouvre le sélecteur de fichiers pour un fichier `.knxproj`
