# Exercice — Préparer et corriger le programme d'un atelier

**Durée :** 45 minutes, consignes et bilan compris. **Organisation :** individuel. **Objectif :** tester et corriger une page web avant de l'enregistrer dans Git, publier une première version, puis corriger des commits locaux en observant les effets sur les fichiers et le staging.

**Prérequis :** Git et identité de commit déjà configurés, compte GitHub avec authentification fonctionnelle, VS Code avec l'extension [Live Server de Ritwick Dey](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) installée avant l'exercice. Savoir repérer une balise HTML et un nom de fichier. Cet exercice autonome réinvestit les commandes Git déjà vues ; il n'ajoute pas automatiquement un créneau au plan de cours.

**Commandes à mobiliser :** `git init`, `git remote add`, `git add`, `git commit`, `git push`, `git status`, `git restore --staged`, `git reset --soft`, `--mixed` et `--hard`.

**À remettre :** l'URL du dépôt GitHub et un fichier de réponses avec les observations du test web et le tableau de l'étape 7. Conserver les réponses **en dehors du dépôt d'exercice**.

## 1. Tester la page, corriger et publier — 17 min

Vous organisez un atelier fictif. Créez un nouveau dossier `atelier-git-exercice`, ouvrez-le dans le terminal et initialisez son dépôt avec une branche appelée `main` : `git init -b main`.

### Préparer les fichiers — 3 min

Ouvrez ce dossier dans VS Code avec **Fichier → Ouvrir le dossier**. Copiez à sa racine les deux fichiers fournis : [index.html](page-git/index.html) et [style.css](page-git/style.css). Gardez leurs noms. La page annonce « Je maîtrise les bases de Git » ; une erreur de liaison empêche volontairement le style de s'appliquer.

Créez dans ce dossier un fichier `programme.txt` contenant exactement :

```text
Atelier Git
Accueil : 09:00
Fin : 12:00
```

Votre dossier contient maintenant `index.html`, `style.css` et `programme.txt`.

### Premier test dans le navigateur — 3 min

Dans **l'explorateur de fichiers de VS Code**, faites un **clic droit sur `index.html` → Open with Live Server**. Le navigateur ouvre la page servie localement. Si l'option manque, vérifiez que Live Server est installé et activé.

Observez : le texte apparaît, mais pas la carte sombre avec les accents verts. Notez ce premier résultat dans vos réponses. **N'exécutez pas encore `add`, `commit` ou `push`.**

### Corriger le lien et retester — 5 min

Ouvrez `index.html` dans l'éditeur. Repérez la balise `<link>` qui charge la feuille de style. Comparez son attribut `href` au nom réel du fichier CSS et corrigez **uniquement le chemin dans `href`** ; ne renommez pas le fichier CSS.

Enregistrez la correction. Revenez dans le navigateur : Live Server actualise normalement la page ; sinon, actualisez-la manuellement. Vérifiez que vous voyez désormais :

- une carte arrondie sur un fond sombre avec un dégradé ;
- le titre « Je maîtrise les bases de Git » avec « Git » en vert menthe ;
- trois encadrés : « Je teste », « Je committe », « Je publie ».

Réduisez la fenêtre : les encadrés doivent s'empiler sur un écran étroit. Notez le chemin avant/après correction et le résultat du second test. **Ne passez à l'enregistrement Git que lorsque le style s'affiche.**

### Enregistrer et publier la version testée — 6 min

Observez les trois fichiers avec `git status`, préparez-les explicitement avec `git add index.html style.css programme.txt` et créez le commit **« Creer la page testee et le programme »**. Vérifiez à nouveau l'état du dépôt.

Sur GitHub, créez un dépôt **vide** nommé `atelier-git-exercice` : sans README, licence ou `.gitignore` ajouté automatiquement. Reliez votre dépôt local à ce dépôt distant avec `git remote add`, sous le nom `origin`, puis publiez `main` avec `git push -u origin main`.

Vérifiez sur GitHub que les trois fichiers apparaissent, que le lien CSS est corrigé dans `index.html` et que `programme.txt` contient les trois lignes attendues. Le push publie les fichiers du dépôt ; il ne déploie pas automatiquement un site web. La page reste testée localement avec Live Server.

**Important pour la suite :** ne poussez plus rien avant l'étape 7. Les commits que vous allez retirer doivent rester locaux. Toutes les manipulations se font dans ce nouveau dépôt d'exercice.

## 2. Retirer une modification du staging — 4 min

Ajoutez cette ligne au fichier et enregistrez-le :

```text
Pause : 10:30
```

Préparez `programme.txt` avec `git add`, puis observez `git status`.

Vous souhaitez finalement retirer cette modification du prochain commit **tout en gardant la ligne dans le fichier**. Utilisez `git restore --staged` sur le fichier.

Vérifiez son état et ouvrez-le dans l'éditeur. Notez où se trouve maintenant la modification. **Ne créez pas encore de commit.**

## 3. Retirer un commit en gardant le travail préparé — 5 min

Préparez à nouveau le fichier et créez le commit **« Ajouter une pause »**.

Retirez ce dernier commit avec **`git reset --soft HEAD~1`**. Ici, `HEAD~1` désigne le parent du commit courant : vous revenez d'un commit en arrière.

Observez `git status` et ouvrez le fichier. La ligne de pause est-elle encore présente ? Est-elle déjà préparée pour un nouveau commit ?

Sans refaire `git add`, créez le commit **« Preciser la pause de l atelier »**. Vérifiez que le dépôt est propre avant de continuer.

## 4. Retirer un commit en gardant le travail non préparé — 5 min

Retirez le commit que vous venez de recréer, cette fois avec **`git reset --mixed HEAD~1`**.

Observez le fichier et `git status`. Comparez avec l'étape précédente : qu'est-ce qui a changé dans le staging ?

Essayez maintenant `git commit -m "Planifier la pause"` **sans refaire `git add`**. Notez le résultat : aucun nouveau commit ne doit être créé.

Effectuez la préparation nécessaire, puis créez réellement le commit **« Planifier la pause »**. Vérifiez que le dépôt est propre avant de continuer.

## 5. Abandonner un essai avec hard — 5 min

Vous allez abandonner uniquement des changements fictifs créés dans cette étape. Vérifiez que vous êtes bien dans `atelier-git-exercice`.

Remplacez la ligne `Fin : 12:00` par `Fin : 18:00`, enregistrez, préparez le fichier et créez le commit **« Tester une fin a 18 heures »**.

Ajoutez ensuite une ligne `Brouillon a supprimer`, enregistrez, mais **ne faites ni add ni commit** pour cet ajout.

Vous décidez d'abandonner l'essai et le brouillon. Exécutez **`git reset --hard HEAD~1`**.

Ouvrez le fichier et lancez `git status`. Notez l'horaire de fin, la présence ou non de la pause et celle du brouillon. Cette commande remplace aussi le contenu des fichiers suivis : la modification non committée peut être perdue.

## 6. Vérifier le résultat local — 4 min

Votre fichier doit maintenant contenir exactement :

```text
Atelier Git
Accueil : 09:00
Fin : 12:00
Pause : 10:30
```

Vérifiez ces quatre lignes et un état propre avec `git status`. Retestez également `index.html` avec Live Server : le style doit toujours s'afficher, car les resets ont conservé la correction du premier commit. Le programme texte est un fichier séparé, il n'est pas affiché automatiquement dans la page HTML. À ce stade, GitHub affiche-t-il déjà la pause dans `programme.txt` ? Vérifiez sur le site et expliquez la différence entre votre fichier local et celui du distant.

## 7. Publier et expliquer — 5 min

Publiez la version finale avec `git push`, puis vérifiez son contenu sur GitHub. **Aucun push forcé n'est nécessaire.**

Complétez le tableau à partir de vos observations faites immédiatement après chaque annulation :

| Manipulation | Contenu observé dans le fichier | Modification préparée pour un commit ? |
|---|---|---|
| `restore --staged` — étape 2 | | |
| `reset --soft HEAD~1` — étape 3 | | |
| `reset --mixed HEAD~1` — étape 4 | | |
| `reset --hard HEAD~1` — étape 5 | | |

Répondez aussi à ces questions :

1. Pourquoi fallait-il refaire `add` après le reset mixed, mais pas après le reset soft ?
2. Qu'est-il arrivé au brouillon non committé lors du reset hard ?
3. Pourquoi la pause n'apparaissait-elle pas sur GitHub avant le dernier push ?

**Critères de réussite :** la page a été testée, corrigée et retestée avant le premier commit ; le style fonctionne ; les trois fichiers et les quatre lignes finales du programme sont publiés ; le dépôt local est propre ; le tableau distingue les trois modes de reset et vous savez expliquer le rôle du staging.