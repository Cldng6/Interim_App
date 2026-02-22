# MVP – Application d'Intérim

## 1. Objectif du MVP
Créer une application web permettant de gérer le cycle de base de l'intérim :
- publication de missions par des entreprises
- candidature d'intérimaires
- gestion simple par une agence / administrateur

Le MVP doit être **fonctionnel, stable et évolutif**, sans fonctionnalités avancées (paie, facturation, signature, etc.).

---

## 2. Cibles utilisateurs

### Intérimaire (Worker)
- créer un compte
- compléter son profil
- consulter les missions disponibles
- postuler à une mission
- suivre le statut de ses candidatures

### Entreprise (Company)
- créer un compte
- créer et gérer ses missions
- consulter les candidatures reçues sur ses propres missions uniquement
- accepter ou refuser un candidat

### Administrateur / Agence
- valider ou refuser les comptes après inscription
- gérer les utilisateurs
- gérer les entreprises
- superviser les missions et candidatures

---

## 3. Fonctionnalités incluses (IN)

### Authentification & sécurité
- inscription (compte inactif en attente de validation)
- validation manuelle du compte par un administrateur
- connexion / déconnexion (uniquement pour les comptes validés)
- gestion des rôles : `ROLE_WORKER`, `ROLE_COMPANY`, `ROLE_ADMIN`
- protection des accès par rôle
- vérification d'ownership : une entreprise ne peut accéder qu'à ses propres missions et candidatures

### Gestion des profils
- profil intérimaire (informations personnelles) — lié au User en OneToOne
- profil entreprise (informations société) — lié au User en OneToOne

### Missions
- création d'une mission
- modification / suppression (réservées à l'entreprise propriétaire)
- statuts : `draft`, `published`, `closed`
- publication / fermeture
- affichage public des missions au statut `published`

### Candidatures
- postuler à une mission
- consulter ses candidatures (intérimaire)
- consulter les candidatures reçues sur ses missions (entreprise propriétaire uniquement)
- statuts : `pending`, `accepted`, `refused`
- changement de statut par l'entreprise

---

## 4. Fonctionnalités exclues (OUT)

❌ Facturation  
❌ Gestion de la paie  
❌ Signature électronique  
❌ Notifications email / SMS  
❌ Matching automatique  
❌ Messagerie interne  
❌ Gestion des contrats  

Ces fonctionnalités pourront être ajoutées dans des versions ultérieures.

---

## 5. Entités principales du MVP

- **User** — authentification, rôle, statut de validation (`pending`, `active`, `rejected`)
- **Worker** — profil intérimaire, lié à User en OneToOne
- **Company** — profil entreprise, lié à User en OneToOne
- **Mission** — besoin d'intérim, lié à Company, statut (`draft`, `published`, `closed`)
- **Candidature** — candidature d'un Worker à une Mission, statut (`pending`, `accepted`, `refused`)

---

## 6. Parcours utilisateur simplifiés

### Parcours intérimaire
1. Création de compte → statut `pending`
2. Validation du compte par l'admin → statut `active`
3. Complétion du profil
4. Consultation des missions publiées
5. Candidature à une mission
6. Suivi du statut de la candidature

### Parcours entreprise
1. Création de compte → statut `pending`
2. Validation du compte par l'admin → statut `active`
3. Création d'une mission (statut `draft`)
4. Publication de la mission (statut `published`)
5. Consultation des candidatures reçues (ses missions uniquement)
6. Acceptation / refus d'un candidat

### Parcours administrateur
1. Consultation des comptes en attente
2. Validation ou refus d'un compte
3. Supervision des missions et candidatures

---

## 7. Stack technique (MVP)

- Backend : Symfony
- ORM : Doctrine
- Templates : Twig
- Frontend : JavaScript
- UI : TailwindCSS
- Base de données : MariaDB

---

## 8. Critères de réussite du MVP

- un utilisateur peut s'inscrire et attendre la validation de son compte
- un admin peut valider ou refuser un compte
- une entreprise validée peut publier une mission
- un intérimaire validé peut postuler à une mission
- une entreprise ne voit que ses propres missions et candidatures
- une candidature peut être acceptée ou refusée
- les accès sont sécurisés par rôle et par ownership

---

## 9. Vision post-MVP (non implémentée)

- gestion d'agence multi-clients
- contrats et documents
- facturation automatisée
- matching par compétences
- notifications email / SMS
- API publique
