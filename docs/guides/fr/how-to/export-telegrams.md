# Comment exporter des télégrammes

SharKNX peut exporter les télégrammes actuellement présents dans la liste de surveillance vers un fichier. Vous pouvez choisir les colonnes à inclure, le nombre de télégrammes, le style d'en-tête des colonnes et le format du délimiteur. Les fichiers exportés peuvent être sauvegardés localement ou partagés directement depuis l'application pour faciliter le **diagnostic KNX** et la gestion de votre **installation domotique**.

---

## Depuis la Monitor Page

1. Démarrez une session de surveillance et laissez les télégrammes s'accumuler, ou arrêtez le moniteur lorsque vous avez capturé le trafic nécessaire à votre **contrôle KNX**.
2. Appuyez sur l'icône **export icon** (en haut à droite de la ligne de la barre de filtrage) pour ouvrir le volet d'exportation.
3. Configurez l'exportation :

   | Option | Description |
   |---|---|
   | **File name** | Pré-rempli avec un horodatage. Modifiez-le pour donner un nom significatif au fichier. |
   | **Columns** | Cochez les colonnes à inclure : ID, Time, Source, Destination, Name\*, Type, Value\*, Raw (\*nécessite un projet ETS chargé) |
   | **Number of telegrams** | Le nombre de télégrammes à exporter (à partir du plus récent). Utilisez cette option pour limiter un grand tampon (buffer) aux N dernières entrées. |
   | **Include column headers** | Activez cette option pour inclure une ligne d'en-tête en haut du fichier CSV. |
   | **Delimiter** | Virgule (par défaut), Tabulation ou Point-virgule. |

4. Appuyez sur **Save** pour enregistrer le fichier sur votre appareil, ou sur **Share** pour ouvrir le volet de partage du système et l'envoyer directement par e-mail, vers un espace de stockage cloud ou une autre application.

---

## Depuis le Shark Hunt Monitor

Le même volet d'exportation est disponible au sein d'une session de surveillance Shark Hunt. Appuyez sur le bouton **save/export button** dans la barre supérieure (actif lorsque des télégrammes sont présents). Toutes les mêmes options s'appliquent.

---

## Remarques

- Les colonnes **Name** et **Value** ne sont significatives que lorsqu'un projet ETS est chargé. Sans projet, ces colonnes seront vides pour la plupart des télégrammes.
- La colonne **Raw** est toujours disponible et contient la charge utile hex brute non analysée — c'est la valeur source réelle que l'application convertit en une valeur lisible par l'homme lorsqu'un projet est chargé.
- L'exportation capture tout ce qui se trouve actuellement dans le tampon de télégrammes. Si le tampon a atteint sa limite (2000 par défaut, configurable dans **Settings → Monitor**), les télégrammes les plus anciens ont déjà été écrasés. Procédez à l'exportation avant que le tampon ne soit plein si vous avez besoin d'une capture plus longue.
- Les fichiers exportés peuvent être réimportés dans le moniteur pour analyse. Depuis le menu **Monitor → tune menu**, utilisez l'option **Import CSV** pour recharger un fichier précédemment exporté dans la liste des télégrammes de vos **bâtiments intelligents**.
