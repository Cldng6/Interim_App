# MVP – Application d’Intérim

## 1. Objectif du MVP
Créer une application web permettant de gérer le cycle de base de l’intérim :
- publication de missions par des entreprises
- candidature d’intérimaires
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
- consulter les candidatures reçues
- accepter ou refuser un candidat

### Administrateur / Agence
- gérer les utilisateurs
- gérer les entreprises
- superviser les missions et candidatures

---

## 3. Fonctionnalités incluses (IN)

### Authentification & sécurité
- inscription
- connexion / déconnexion
- gestion des rôles
- protection des accès par rôle

### Gestion des profils
- profil intérimaire (informations personnelles)
- profil entreprise (informations société)

### Missions
- création d’une mission
- modification / suppression
- publication / fermeture
- affichage public des missions actives

### Candidatures
- postuler à une mission
- consulter ses candidatures
- changement de statut (en attente, acceptée, refusée)

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

- User (authentification et rôles)
- Worker (profil intérimaire)
- Company (profil entreprise)
- Mission (besoin d’intérim)
- Application (candidature)

---

## 6. Parcours utilisateur simplifiés

### Parcours intérimaire
1. Création de compte
2. Complétion du profil
3. Consultation des missions
4. Candidature à une mission
5. Suivi du statut

### Parcours entreprise
1. Création de compte
2. Création d’une mission
3. Publication
4. Consultation des candidatures
5. Acceptation / refus

---

## 7. Stack technique (MVP)

- Backend : Symfony
- ORM : Doctrine
- Templates : Twig
- Frontend : JavaScript
- UI : TailwindCSS
- Base de données : Mariadb

---

## 8. Critères de réussite du MVP

- un utilisateur peut s’inscrire et se connecter
- une entreprise peut publier une mission
- un intérimaire peut postuler
- une candidature peut être acceptée ou refusée
- les accès sont sécurisés par rôle

---

## 9. Vision post-MVP (non implémentée)
- gestion d’agence multi-clients
- contrats et documents
- facturation automatisée
- matching par compétences
- API publique
