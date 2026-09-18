# Atelier — Prendre en main une API avec Bruno

Module **CAP — Concevoir une API REST**. Coda Dijon, B2.

Avant d'écrire votre propre contrat, vous explorez une API **déjà conçue** : vous lui
envoyez des requêtes avec Bruno et vous observez ce qu'elle répond. Le contrat fourni
est le *Train Travel API* — une API de réservation de trajets en train.

## Démarrer

Placez-vous dans ce dossier, puis lancez le mock :

```bash
cd atelier-bruno
docker compose up
```

L'API est servie en local sur `http://localhost:4010`. Prism la sert depuis le contrat :
pas de dépendance à un service en ligne.

La documentation du contrat, elle, est servie sur `http://localhost:4011` : le même
YAML, rendu lisible plutôt que consulté en brut.

## Une API protégée

Cette API demande une **authentification**. Sans jeton, elle refuse :

```bash
curl http://localhost:4010/stations
# -> 401 Unauthorized (problem+json)
```

Ajoutez un en-tête `Authorization` et elle répond :

```bash
curl -H 'Authorization: Bearer demo-token' http://localhost:4010/stations
# -> 200, la liste des gares
```

Le mock ne vérifie pas la *valeur* du jeton, seulement sa **présence** — n'importe quelle
chaîne fait l'affaire. Dans Bruno, ce jeton se pose une fois dans l'onglet **Auth** de la
requête (type *Bearer*).

## Ce que vous produisez

Votre collection Bruno se crée **dans ce dossier**. Une collection est un dossier de
fichiers texte : elle se commit, se relit dans un `diff` et se partage comme du code.

C'est tout l'intérêt face à une commande jetée dans un terminal.

## Attribution

Le contrat de cette API n'est pas de nous. Voir [`NOTICE.md`](NOTICE.md) pour l'auteur
et la licence.
