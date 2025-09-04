# Gestion Scolaire Offline

Application web monopage (SPA) fonctionnant entièrement hors ligne (localStorage) pour la gestion basique :
- Classes
- Élèves
- Compétences & niveaux
- Évaluations / Notes
- Absences
- Export des données (JSON + ZIP)

## Objectifs
Fournir un outil léger utilisable sans connexion réseau après première ouverture (PWA à venir).

## Fonctionnalités actuelles
- Création / édition / suppression de classes
- Ajout d'élèves dans une classe
- Gestion des compétences (par classe)
- Création d'évaluations associées à des compétences
- Attribution de notes (0–20) par élève et par évaluation
- Marquage d'absences par date
- Export JSON complet
- Export ZIP (JSON + fichiers générés) via JSZip CDN
- Thème clair / sombre (préférence stockée)
- Sauvegarde locale automatique après chaque action

## À venir
- Import JSON (fusion / remplacement) (TODO)
- Éditeur visuel du plan de classe (drag & drop) (TODO)
- PWA (manifest + service worker + cache) (TODO)
- Statistiques (moyennes par compétence / élève) (TODO)

## Structure
```
/
├── index.html
├── css/
│   └── style.css
├── js/
│   ├── app.js         (initialisation, événements)
│   ├── models.js      (structures de données / helpers)
│   ├── storage.js     (lecture/écriture localStorage)
│   ├── ui.js          (rendu dynamique)
│   └── export.js      (export JSON / ZIP)
├── data/
│   └── seed.json      (jeu de données initial minimal facultatif)
├── LICENSE
├── .gitignore
└── README.md
```

## Données
Tout est stocké sous la clé `school_manager_data_v1` dans localStorage :
```
{
  classes: [
    {
      id, name, students: [{ id, firstName, lastName }],
      competences: [{ id, label, description }],
      evaluations: [{ id, title, date, competenceId }],
      notes: [{ id, studentId, evaluationId, value }],
      absences: [{ id, studentId, dateISO }]
    }
  ],
  settings: { theme: "light" | "dark" }
}
```

## Export
- JSON : fichier unique complet
- ZIP : contient data.json (et pourra plus tard inclure d’autres artefacts)

## Licence
MIT — voir LICENSE.

## Sécurité / Confidentialité
Aucune donnée transmise à un serveur. À n’utiliser que pour des données non sensibles ou avec consentement adéquat.

## Script de démarrage simple (serveur local optionnel)
Vous pouvez simplement ouvrir `index.html` dans un navigateur moderne.  
Pour contourner certains blocages de modules futurs :  
`python3 -m http.server 8000` puis http://localhost:8000

## TODO marqués dans le code
Chercher "TODO:" dans les fichiers js.
