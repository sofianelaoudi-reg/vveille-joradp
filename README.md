# veille-joradp

Veille automatique du Journal Officiel algérien (édition française, joradp.dz).
Trois fois par jour (7h, 12h, 15h, heure d'Alger), un workflow GitHub Actions
détecte les nouveaux numéros, en génère un résumé et l'envoie par e-mail (Gmail).

## Mise en place

1. Créer les secrets du dépôt (Settings → Secrets and variables → Actions) :
   - `GMAIL_USER` : adresse Gmail expéditrice
   - `GMAIL_APP_PASSWORD` : mot de passe d'application Google (16 caractères)
   - `MAIL_TO` : destinataire (facultatif)
   - `ANTHROPIC_API_KEY` : pour le résumé automatique (facultatif)
2. Onglet Actions → « Veille JORADP » → Run workflow, pour un premier test.
   Au premier passage, le dernier numéro existant est enregistré sans e-mail.
3. Pour fixer le point de départ : `python veille_joradp.py --init 2026 68`
   puis déposer le `state.json` produit.

## Fichiers

- `veille_joradp.py` : le script
- `.github/workflows/veille.yml` : la planification
- `state.json` : dernier numéro traité (créé et mis à jour automatiquement)

Aucun secret ne doit figurer dans le code : tout passe par les secrets GitHub.
