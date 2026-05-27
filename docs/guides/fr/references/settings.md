# Référence des paramètres

La page **Settings** est accessible depuis n’importe quel écran en appuyant sur l’icône **gear icon** (⚙️) en haut à droite de la barre d’application.

La page regroupe toutes les options configurables en sections. Une icône de **search icon** (🔍) dans la barre supérieure permet d’accéder directement à une section par son nom.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-overview.png" width="320" alt="Settings page — full section list" />
</div>

---

## Discover Settings

Contrôle la manière dont l’application recherche et se connecte aux KNX IP gateways sur le réseau dans un contexte de **domotique KNX**, d’installation domotique et de **diagnostic KNX**.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-a.png" width="320" alt="Discover Settings (1 of 2)" /></td>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-b.png" width="320" alt="Discover Settings (2 of 2)" /></td>
    </tr>
  </table>
</div>

### Multicast

| Setting | Default | Description |
|---|---|---|
| Multicast address | `224.0.23.12` | L’adresse multicast IP utilisée pour la découverte KNX IP et le routage IP. Ne modifiez cette valeur que si votre réseau utilise un groupe multicast non standard. |
| Multicast port | `3671` | Le port UDP utilisé pour la découverte multicast et les communications de routage. |

### Discovery behaviour

| Setting | Default | Description |
|---|---|---|
| Always show multicast options | Off | Lorsque activé, les options multicast sont toujours visibles dans l’onglet Discover. Lorsque désactivé, elles n’apparaissent que si un KNX IP Router avec capacités de routage est détecté lors d’un scan. |
| Force unicast subnet scan | Off | Lorsque activé, après l’envoi des requêtes multicast de découverte, l’application envoie également des requêtes unicast à chaque IP du sous-réseau. Utile sur les réseaux Wi-Fi où le multicast peut être filtré. Si aucune gateway n’est trouvée via multicast, un scan unicast est automatiquement exécuté en fallback. |

### Timeouts

| Setting | Default | Min | Max | Description |
|---|---|---|---|---|
| Discovery timeout | 3 s | 1 s | 10 s | Temps d’attente des réponses après une requête de découverte. À augmenter sur les réseaux lents ou congestionnés. |
| Connection timeout | 3 s | 1 s | 10 s | Temps d’attente pour établir une connexion de tunneling vers une gateway avant de la considérer comme inaccessible. |

---

## Project Settings

Contrôle la manière dont les fichiers de projet ETS sont analysés et affichés dans des systèmes de **bâtiments intelligents** et de contrôle KNX.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-project.png" width="320" alt="Project Settings" />
</div>

| Setting | Default | Description |
|---|---|---|
| Load communication objects | On | Lorsque activé, l’application analyse et stocke les communication objects pour chaque device ayant au moins une adresse de groupe connectée. Désactiver réduit la mémoire utilisée sur les grands projets mais supprime la vue Communication Objects dans la page Project. |
| Items per page | 50 | Min: 20 · Max: 200 — Nombre d’éléments affichés lors de l’expansion d’une liste dans l’arborescence du projet. Une fois la limite atteinte, un bouton **Load more** apparaît. |

---

## Monitor Settings

Contrôle le comportement du bus monitor KNX pour le **diagnostic KNX**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-monitor.png" width="320" alt="Monitor Settings" />
</div>

| Setting | Default | Description |
|---|---|---|
| Keep screen on | On | Empêche l’écran de s’éteindre pendant une session de monitoring. Recommandé car les OS mobiles ferment souvent les connexions IP lorsque l’écran s’éteint. |
| Telegram buffer size | 2000 | Min: 50 · Max: 5000 — Nombre maximum de télégrammes conservés dans le monitor. Les plus anciens sont écrasés lorsque la limite est atteinte. |

---

## Scan Settings

Contrôle le scan du mode programmation dans **Management → Prog. Mode**, utilisé pour le **contrôle KNX**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-scan.png" width="320" alt="Scan Settings" />
</div>

| Setting | Default | Min | Max | Description |
|---|---|---|---|---|
| Scan duration | 10 s | 4 s | 20 s | Durée totale d’un scan en mode programmation. |
| Scan interval | 2 s | 1 s | 4 s | Fréquence d’envoi des signaux de scan pendant la session. |

---

## Subscription

Affiche l’état de l’abonnement et les options de gestion.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-subscription.png" width="320" alt="Subscription" />
</div>

| Item | Description |
|---|---|
| Current plan | Plan actif : **Free**, **Monthly**, **Yearly**, ou **Lifetime**. |
| Restore purchases | Restaure un abonnement après réinstallation ou changement d’appareil. |
| Cancel subscription | Ouvre la page de gestion App Store / Google Play. |
| Privacy Policy | Lien vers la Privacy Policy. |
| Terms of Service | Lien vers les Terms of Service. |

---

## Language

Liste des langues disponibles dans l’application. Le changement est immédiat.

- 🇬🇧 English  
- 🇩🇪 German  
- 🇫🇷 French  
- 🇪🇸 Spanish  
- 🇮🇹 Italian  

---

## Theme

Définit le thème visuel de l’application.

| Option | Description |
|---|---|
| Light | Thème clair permanent |
| Dark | Thème sombre permanent |
| Match system | Suit le système |

---

## Send Feedback

| Option | Description |
|---|---|
| Leave a review | Ouvre la page store |
| Report a bug | Email vers info@owl-automata.com |
| Write to us | Email général |

> Voir aussi: [How to Report an Issue](../../../support/how-to-report-an-issue.md)

---

## About

Affiche la version de l’application et les informations de copyright.
