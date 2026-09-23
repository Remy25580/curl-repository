# Inventaire des points d'entrée

Le livrable de l'atelier d'analyse. Il dit ce que l'API devra **permettre** — pas comment on
l'écrira.

Une règle : tout ce qui figure ici doit se justifier par la lettre de mission ou par un écran
des maquettes. Si vous ne savez plus d'où vient une ligne, c'est peut-être qu'elle n'en vient
pas. (Seule exception : la section bonus, si vous en ajoutez une.)

---

## Ce que l'utilisateur peut faire

Une action par ligne, en français. Pas encore de chemins.

- L'utilisateur peut consulter les villes déservies par l'Office sans être connecté.
- L'utilisateur peut rechercher un lancer sans être connecté.
- L'utilisateur peut se créer un compte voyageur auprès de l'Office.
- L'utilisateur peut se connecter à son compte voyageur.
- L'utilisateur connecté peut consulter ses informations personnelles et ses billets.
- L'utilisateur peut consulter son panier actuel.
- L'utilisateur peut saisir une ville de départ.
- L'utilisateur peut saisir une ville d'arrivée.
- L'utilisateur peut saisir une date.
- L'utilisateur peut saisir un nombre de voyageurs.
- L'utilisateur peut modifier les informations saisies pour son lancer.
- L'utilisateur peut consulter le détail d'un lancer.
- L'utilisateur peut placer un lancer dans son panier.
- L'utilisateur peut valider son panier.
- L'utilisateur peut choisir de payer ses billets en carte bancaire ou en bon de transport de l'Office
- L'utilisateur peut payer ses billets.

## Les points d'entrée

| Ce que ça fait | Chemin proposé | Qui peut l'appeler |
|---|---|---|
| Voir les villes déservies |GET /villes| Tout le monde |
| Rechercher un trajet |GET /trajets| Tout le monde |
| Se connecter à son compte |POST /connexion| Utilisateurs ayant un compte |
| S'inscrire auprès de l'office |POST /inscription| Tout le monde |
| Consulter ses informations perso |GET /users/me| Utilisateurs connectés |
| Consulter ses billets|GET /users/me/billets| Utilisateurs connectés |
| Consulter son panier |GET /users/me/panier| Utilisateurs connectés |
| Spécifier une ville de départ |GET /trajets?depart=...| Tout le monde |
| Spécifier une ville d'arrivée |GET /trajets?arrivee=...| Tout le monde |
| Spécifier une date de lancer |GET /trajets?date=...| Tout le monde |
| Spécifier un nombre de voyageurs |GET /trajets?voyageurs=...| Tout le monde |
| Consulter le détail d'un lancer |GET /trajets/{id} | Tout le monde |
| Placer un lancer dans son panier |POST /users/me/panier | Utilisateurs connectés |
| Valider son panier |POST users/me/payments | Utilisateurs connectés |
| Payer |POST users/me/billets | Utilisateurs connectés |

## Les données qui circulent

Pour chaque point d'entrée : ce qu'il reçoit, ce qu'il renvoie. Nommez les données comme
l'Office les nomme — les traduire en identifiants techniques, c'est le travail de demain.

### GET /villes

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: La liste des villes

### GET /trajets

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: La liste des lancers

### POST /connexion

=> Ce qu'il reçoit: Les informations de login
=> Ce qu'il renvoie: Un message de succès/échec

### POST /inscription

=> Ce qu'il reçoit: Les informations du nouvel utilisateur
=> Ce qu'il renvoie: Un message de succès/échec

### GET /users/me

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: Les informations du profil de l'utilisateur

### GET /users/me/billets

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: Les billets de l'utilisateur

### GET /users/me/panier

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: Le panier de l'utilisateur

### GET /trajets?depart=...

=> Ce qu'il reçoit: La querry ```depart```
=> Ce qu'il renvoie: La liste des lancers partant de ```depart```

### GET /trajets?arrivee=...

=> Ce qu'il reçoit: La querry ```arrivee```
=> Ce qu'il renvoie: La liste des lancers atterissant à ```arrivee```

### GET /trajets?date=...

=> Ce qu'il reçoit: La querry ```date```
=> Ce qu'il renvoie: La liste des lancers le ```date```

### GET /trajets?voyageurs=...

=> Ce qu'il reçoit: La querry ```voyageurs```
=> Ce qu'il renvoie: La liste des lancers prenant en charge ```voyageurs``` voyageurs

### GET /trajets/:id

=> Ce qu'il reçoit: Rien
=> Ce qu'il renvoie: Les détails d'un trajet

### POST /users/me/panier

=> Ce qu'il reçoit: Les informations d'un/de plusieurs lancer(s)
=> Ce qu'il renvoie: Le panier de l'utilisateur updaté

### POST users/me/payments

=> Ce qu'il reçoit: Les informations des lancers du panier de l'utilisateur
=> Ce qu'il renvoie: Les lancers à payer

### POST users/me/billets

=> Ce qu'il reçoit: Les informations de paiement de l'utilisateur
=> Ce qu'il renvoie: Les billets fraichement payés dans l'onglet des billets de l'utilisateur

## Ce dont on n'est pas sûrs

Les questions que la lettre et les maquettes ne tranchent pas. Une question notée vaut mieux
qu'une réponse inventée.

- Est on sensé pouvoir supprimer un lancer du panier ?
- Est il sensé y avoir une section spéciale pour modifier les informations de recherche d'un lancer ?
- Est on sensé pouvoir supprimer son compte ?