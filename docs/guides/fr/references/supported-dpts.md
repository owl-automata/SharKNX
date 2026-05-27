# Types de points de données (DPT) pris en charge

SharKNX prend en charge les types de points de données KNX dans deux contextes pour votre installation domotique :

- **Décodage** — valeurs décodées et affichées lors de la réception de télégrammes dans le Monitor. S'applique à tous les DPT de ce document pour un diagnostic KNX précis.
- **Envoi** — DPT disponibles pour la sélection lors de la composition d'une commande. Un sous-ensemble des DPT décodables pour le contrôle KNX. Marqués par ✅ dans le tableau ci-dessous.

Si un télégramme arrive pour une adresse de groupe dont le DPT est inconnu ou n'est pas encore pris en charge, la charge utile hex brute est affichée au lieu d'une valeur décodée.

---

## Aperçu

| DPT | Nom | Taille | Envoi |
|-----|------|------|------|
| **1** | Booléen 1 bit | 1 bit | ✅ |
| **2** | Contrôlé 1 bit | 2 bits | ✅ |
| **3** | Contrôlé 3 bits (Pas) | 4 bits | ✅ |
| **4** | Caractère | 1 octet | ✅ |
| **5** | Valeur non signée 8 bits | 1 octet | ✅ |
| **6** | Valeur signée 8 bits | 1 octet | ✅ |
| **7** | Valeur non signée 2 octets | 2 octets | ✅ |
| **8** | Valeur signée 2 octets | 2 octets | ✅ |
| **9** | Flottant 2 octets | 2 octets | ✅ |
| **10** | Heure du jour | 3 octets | ✅ |
| **11** | Date | 3 octets | ✅ |
| **12** | Valeur non signée 4 octets | 4 octets | ✅ |
| **13** | Valeur signée 4 octets | 4 octets | ✅ |
| **14** | Flottant IEEE 754 4 octets | 4 octets | ✅ |
| **15** | Accès d'entrée | 4 octets | — |
| **16** | Chaîne de 14 caractères | 14 octets | ✅ |
| **17** | Numéro de scène | 1 octet | ✅ |
| **18** | Contrôle de scène | 1 octet | ✅ |
| **19** | Date et heure | 8 octets | ✅ |
| **20** | Énumération 1 octet | 1 octet | ✅ |
| **21** | Statut / Indicateurs 8 bits | 1 octet | ✅ |
| **22** | Statut / Indicateurs 16 bits | 2 octets | ✅ |
| **23** | Ensemble 2 bits | 1 octet | — |
| **24** | Chaîne variable (ISO 8859-1) | variable | — |
| **25** | Double quartet | 1 octet | — |
| **26** | Info de scène | 1 octet | — |
| **27** | Info combinée 32 bits | 4 octets | — |
| **28** | Chaîne variable (UTF-8) | variable | ✅ |
| **29** | Valeur signée 8 octets | 8 octets | ✅ |
| **30** | Activation de canal (24 ch) | 3 octets | — |
| **206** | Délai + Mode CVC | 3 octets | — |
| **217** | Version | 2 octets | — |
| **219** | Info d'alarme | 6 octets | — |
| **222** | Consignes de température (×3) | 6 octets | — |
| **225** | Temps de pas de mise à l'échelle | 4 octets | — |
| **229** | Valeur de comptage | 6 octets | — |
| **232** | Couleur RGB | 3 octets | ✅ |
| **234** | Code de langue | 2 octets | — |
| **235** | Énergie active de tarif | 6 octets | — |
| **240** | Position combinée (stores) | 3 octets | — |
| **241** | Statut de l'actionneur de volet | 4 octets | — |
| **242** | Couleur CIE xyY | 6 octets | ✅ |
| **243** | Transition de couleur xyY | 8 octets | — |
| **249** | Luminosité et transition CCT | 6 octets | ✅ |
| **250** | Contrôle de la luminosité et CCT (relatif) | 3 octets | ✅ |
| **251** | Couleur RGBW | 6 octets | ✅ |
| **252** | Contrôle relatif RGBW | 5 octets | ✅ |
| **253** | Contrôle relatif xyY | 4 octets | — |
| **254** | Contrôle relatif RGB | 3 octets | ✅ |
| **275** | Quatre flottants de 2 octets | 8 octets | — |

---

## Sous-types

Les sections suivantes répertorient les sous-types sélectionnables lors de l'**envoi** de commandes pour le contrôle KNX, regroupés par type principal. Les DPT avec un seul sous-type ou sans prise en charge d'envoi sont omis.

### DPT 1 — Booléen 1 bit

| Sous-type | Description |
|---------|-------------|
| 1.001 | Commutation (Off / On) |
| 1.002 | Booléen |
| 1.003 | Activation |
| 1.004 | Rampe |
| 1.005 | Alarme |
| 1.006 | Valeur binaire |
| 1.007 | Pas |
| 1.008 | Haut / Bas |
| 1.009 | Ouvrir / Fermer |
| 1.010 | Démarrer / Arrêter |
| 1.011 | État |
| 1.012 | Inverser |
| 1.013 | Style d'envoi de variation |
| 1.014 | Source d'entrée |
| 1.015 | Réinitialisation |
| 1.016 | Acquittement |
| 1.017 | Déclencheur |
| 1.018 | Présence |
| 1.019 | Fenêtre / Porte |
| 1.021 | Fonction logique |
| 1.022 | Scène A/B |
| 1.023 | Mode volets / stores |
| 1.100 | Refroidissement / Chauffage |

### DPT 2 — Contrôlé 1 bit

| Sous-type | Description |
|---------|-------------|
| 2.001 | Contrôle de commutation |
| 2.002 | Contrôle booléen |
| 2.003 | Contrôle d'activation |
| 2.004 | Contrôle de rampe |
| 2.005 | Contrôle d'alarme |
| 2.006 | Contrôle de valeur binaire |
| 2.007 | Contrôle de pas |
| 2.008 | Contrôle de direction 1 |
| 2.009 | Contrôle de direction 2 |
| 2.010 | Contrôle de démarrage |
| 2.011 | Contrôle d'état |
| 2.012 | Contrôle d'inversion |

### DPT 3 — Contrôlé 3 bits

| Sous-type | Description |
|---------|-------------|
| 3.007 | Contrôle de variation |
| 3.008 | Contrôle de stores |

### DPT 4 — Caractère

| Sous-type | Description |
|---------|-------------|
| 4.001 | Caractère (ASCII) |
| 4.002 | Caractère (ISO 8859-1) |

### DPT 5 — Valeur non signée 8 bits

| Sous-type | Description | Plage | Unité |
|---------|-------------|-------|------|
| 5.001 | Mise à l'échelle / Pourcentage | 0–100 | % |
| 5.003 | Angle | 0–360 | ° |
| 5.004 | Pourcentage | 0–255 | % |
| 5.005 | Ratio | 0–255 | — |
| 5.006 | Tarif | 0–255 | — |
| 5.010 | Impulsions de compteur | 0–255 | — |

### DPT 6 — Valeur signée 8 bits

| Sous-type | Description | Plage | Unité |
|---------|-------------|-------|------|
| 6.001 | Pourcentage | −128–127 | % |
| 6.010 | Impulsions de compteur | −128–127 | — |

### DPT 7 — Valeur non signée 2 octets

| Sous-type | Description | Unité |
|---------|-------------|------|
| 7.001 | Impulsions | — |
| 7.002 | Période de temps | ms |
| 7.003 | Période de temps | 10 ms |
| 7.004 | Période de temps | 100 ms |
| 7.005 | Période de temps | s |
| 7.006 | Période de temps | min |
| 7.007 | Période de temps | h |
| 7.011 | Longueur | mm |
| 7.012 | Courant | mA |
| 7.013 | Luminosité | lux |
| 7.600 | Température de couleur | K |

### DPT 8 — Valeur signée 2 octets

| Sous-type | Description | Unité |
|---------|-------------|------|
| 8.001 | Différence d'impulsions | — |
| 8.002 | Décalage temporel | ms |
| 8.003 | Décalage temporel | 10 ms |
| 8.004 | Décalage temporel | 100 ms |
| 8.005 | Décalage temporel | s |
| 8.006 | Décalage temporel | min |
| 8.007 | Décalage temporel | h |
| 8.010 | Différence de pourcentage | % |
| 8.011 | Angle de rotation | ° |

### DPT 9 — Flottant 2 octets

| Sous-type | Description | Unité |
|---------|-------------|------|
| 9.001 | Température | °C |
| 9.002 | Différence de température | K |
| 9.003 | Changement de température | K/h |
| 9.004 | Éclairement | lux |
| 9.005 | Vitesse du vent | m/s |
| 9.006 | Pression | Pa |
| 9.007 | Humidité | % |
| 9.008 | Qualité de l'air (CO₂) | ppm |
| 9.009 | Flux d'air | m³/h |
| 9.010 | Temps | s |
| 9.011 | Temps | ms |
| 9.020 | Tension | mV |
| 9.021 | Courant | mA |
| 9.022 | Densité de puissance | W/m² |
| 9.023 | Kelvin par pourcentage | K/% |
| 9.024 | Puissance | kW |
| 9.025 | Débit volumique | l/h |
| 9.026 | Quantité de pluie | l/m² |
| 9.027 | Température | °F |
| 9.028 | Vitesse du vent | km/h |

### DPT 13 — Valeur signée 4 octets

| Sous-type | Description | Unité |
|---------|-------------|------|
| 13.001 | Impulsions de compteur | — |
| 13.002 | Débit | m³/h |
| 13.010 | Énergie active | Wh |
| 13.011 | Énergie apparente | VAh |
| 13.012 | Énergie réactive | VARh |
| 13.013 | Énergie active | kWh |
| 13.014 | Énergie apparente | kVAh |
| 13.015 | Énergie réactive | kVARh |
| 13.100 | Décalage temporel | s |

### DPT 14 — Flottant IEEE 4 octets (sous-types sélectionnés)

Seul un sous-ensemble des 80 sous-types du DPT 14 est disponible dans l'interface d'envoi (send UI). Tous les sous-types sont décodés dans le Monitor pour assurer un diagnostic KNX complet.

| Sous-type | Description | Unité |
|---------|-------------|------|
| 14.007 | Angle | ° |
| 14.019 | Courant électrique | A |
| 14.027 | Potentiel électrique | V |
| 14.033 | Fréquence | Hz |
| 14.056 | Puissance | W |
| 14.065 | Vitesse | m/s |
| 14.068 | Température | °C |
| 14.069 | Température absolue | K |
| 14.070 | Différence de température | K |

### DPT 16 — Chaîne de 14 caractères

| Sous-type | Description |
|---------|-------------|
| 16.000 | ASCII |
| 16.001 | ISO 8859-1 |

### DPT 20 — Énumération 1 octet

| Sous-type | Description |
|---------|-------------|
| 20.002 | Mode bâtiment |
| 20.003 | Mode occupation |
| 20.004 | Priorité |
| 20.005 | Mode d'application d'éclairage |
| 20.006 | Zone d'application d'éclairage |
| 20.007 | Type de classe d'alarme |
| 20.008 | Mode d'alimentation (PSU) |
| 20.013 | Temporisation |
| 20.014 | Force du vent (Beaufort) |
| 20.100 | Type de carburant |
| 20.101 | Type de brûleur |
| 20.102 | Mode CVC |
| 20.103 | Mode ECS |
| 20.104 | Priorité de charge |
| 20.105 | Mode de contrôle CVC |
| 20.106 | Mode d'urgence CVC |
| 20.107 | Mode de basculement |
| 20.108 | Mode de vanne |
| 20.109 | Mode de registre |
| 20.110 | Mode de chauffage |
| 20.111 | Mode de ventilateur |
| 20.112 | Mode Maître / Esclave |
| 20.113 | Statut de consigne de la pièce |

> **Remarque :** L'affichage des étiquettes d'énumération pour la plupart des sous-types du DPT 20 se rabat sur le numéro de mode brut (raw). Des étiquettes nommées (par ex. "Comfort", "Standby") sont affichées pour le 20.102 (Mode CVC) et quelques autres au sein des bâtiments intelligents.

### DPT 21 — Indicateurs de statut 8 bits

| Sous-type | Description |
|---------|-------------|
| 21.001 | Statut général |
| 21.002 | Contrôle du participant |
| 21.100 | Signal de forçage |
| 21.102 | Statut du contrôleur de chauffage de pièce |
| 21.103 | Statut du contrôleur ECS solaire |
| 21.105 | Statut du contrôleur de refroidissement de pièce |
| 21.106 | Statut du contrôleur de ventilation |

### DPT 22 — Indicateurs de statut 16 bits

| Sous-type | Description |
|---------|-------------|
| 22.100 | Statut du contrôleur ECS |
| 22.101 | Statut RHCC |

### DPT 29 — Valeur signée 8 octets (Énergie 64 bits)

| Sous-type | Description | Unité |
|---------|-------------|------|
| 29.010 | Énergie active | Wh |
| 29.011 | Énergie apparente | VAh |
| 29.012 | Énergie réactive | VARh |

### DPT 232 / 242 / 249 / 250 / 251 / 252 / 254 — Couleur et Éclairage

| DPT | Description | Taille |
|-----|-------------|------|
| 232.600 | Couleur RGB | 3 octets |
| 242.600 | Couleur CIE xyY | 6 octets |
| 249.600 | Luminosité et transition de température de couleur | 6 octets |
| 250.600 | Contrôle de la luminosité et de la température de couleur (relatif) | 3 octets |
| 251.600 | Couleur RGBW | 6 octets |
| 252.600 | Contrôle relatif RGBW | 5 octets |
| 254.600 | Contrôle relatif RGB | 3 octets |

---

## DPT pour décodage uniquement

Les DPT suivants sont décodés dans le Monitor lorsque le projet ETS fournit l'attribution du DPT, mais ne sont pas disponibles pour la composition manuelle de commandes dans l'interface d'envoi (send UI) de votre domotique KNX.

| DPT | Description |
|-----|-------------|
| 15.000 | Accès d'entrée (code d'accès) |
| 23.x | Ensemble d'actions 2 bits (on/off, haut/bas, alarme) |
| 24.x | Chaîne de longueur variable (ISO 8859-1) |
| 25.x | Double quartet |
| 26.001 | Info de scène |
| 27.001 | Info combinée par bits On/Off |
| 30.1010 | Activation de canal (24 canaux) |
| 206.x | Délai + Mode CVC/ECS/Occupation/Bâtiment |
| 217.001 | Version de DPT |
| 219.001 | Info d'alarme |
| 222.x | Consignes de température ambiante (×3) |
| 225.x | Temps de pas de mise à l'échelle |
| 229.001 | Valeur de comptage |
| 234.001 | Code de langue (ISO 639-1) |
| 235.001 | Énergie active de tarif |
| 240.800 | Position combinée (stores/volets) |
| 241.800 | Statut de l'actionneur de volet |
| 243.x | Transition de couleur xyY |
| 253.x | Contrôle relatif xyY |
| 275.x | Quatre flottants de 2 octets |
