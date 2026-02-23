# Propriétés des entités

---

## User
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| email | string | unique, utilisé pour la connexion |
| password | string | hashé |
| roles | array | `ROLE_WORKER`, `ROLE_COMPANY`, `ROLE_ADMIN` |
| status | string | `pending`, `active`, `rejected` |
| createdAt | datetime | date d'inscription |
| updatedAt | datetime | dernière mise à jour |

---

## Worker *(OneToOne → User)*
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| user | User | OneToOne |
| firstName | string | prénom |
| lastName | string | nom de famille |
| phone | string | numéro de téléphone |
| address | string | adresse postale |
| city | string | ville |
| zipCode | string | code postal |
| dateOfBirth | date | date de naissance |
| skills | text | compétences (texte libre) |
| cvFilename | string | nom du fichier CV uploadé (nullable) |
| createdAt | datetime | |
| updatedAt | datetime | |

---

## Company *(OneToOne → User)*
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| user | User | OneToOne |
| companyName | string | raison sociale |
| siret | string | numéro SIRET (14 chiffres) |
| address | string | adresse du siège |
| city | string | ville |
| zipCode | string | code postal |
| sector | string | secteur d'activité |
| phone | string | téléphone |
| website | string | site web (nullable) |
| createdAt | datetime | |
| updatedAt | datetime | |

---

## Mission *(ManyToOne → Company)*
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| company | Company | ManyToOne |
| title | string | intitulé du poste |
| description | text | détail de la mission |
| city | string | lieu de la mission |
| startDate | date | date de début |
| endDate | date | date de fin (nullable) |
| hourlyRate | decimal | taux horaire (nullable) |
| contractType | string | `interim`, `cdd`, `cdii` |
| slots | int | nombre de postes disponibles (défaut : 1) |
| status | string | `draft`, `published`, `closed` |
| createdAt | datetime | |
| updatedAt | datetime | |

---

## Candidature *(ManyToOne → Worker, ManyToOne → Mission)*
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| worker | Worker | ManyToOne |
| mission | Mission | ManyToOne |
| coverLetter | text | message de motivation (nullable) |
| status | string | `pending`, `accepted`, `refused` |
| createdAt | datetime | date de candidature |
| updatedAt | datetime | dernière mise à jour du statut |

---

## Contraintes notables
- Un Worker ne peut postuler qu'une seule fois à la même Mission → contrainte d'unicité sur `(worker, mission)`
- Une Mission ne peut être modifiée que par la Company propriétaire (ownership)
- Une Candidature ne peut être consultée que par le Worker concerné ou la Company propriétaire de la Mission
