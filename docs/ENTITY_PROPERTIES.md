# Propriétés des entités – MVP Intérim

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

## Media *(OneToOne → Worker, côté Media)*
| Propriété | Type | Notes |
|---|---|---|
| id | int | clé primaire |
| worker | Worker | OneToOne, nullable (clé étrangère portée par Media) |
| filename | string | nom du fichier généré (stocké sur le filesystem) |
| originalName | string | nom d'origine du fichier uploadé |
| mimeType | string | ex : `image/jpeg`, `image/png` |
| size | int | taille en octets |
| type | string | contexte : `worker_avatar` |
| createdAt | datetime | date d'upload |

---

## Contraintes notables
- Un Worker ne peut postuler qu'une seule fois à la même Mission → contrainte d'unicité sur `(worker, mission)`
- Une Mission ne peut être modifiée que par la Company propriétaire (ownership)
- Une Candidature ne peut être consultée que par le Worker concerné ou la Company propriétaire de la Mission



# MPD – MVP Intérim

---

## user
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| email | NOT NULL, UNIQUE |
| password | NOT NULL |
| roles | NOT NULL |
| status | NOT NULL, défaut `pending` |
| created_at | NOT NULL |
| updated_at | NOT NULL |

---

## worker
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| **user_id** (FK → user.id) | NOT NULL, UNIQUE |
| first_name | NOT NULL |
| last_name | NOT NULL |
| phone | NULL |
| address | NULL |
| city | NULL |
| zip_code | NULL |
| date_of_birth | NULL |
| skills | NULL |
| cv_filename | NULL |
| created_at | NOT NULL |
| updated_at | NOT NULL |

---

## company
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| **user_id** (FK → user.id) | NOT NULL, UNIQUE |
| company_name | NOT NULL |
| siret | NOT NULL, UNIQUE |
| address | NULL |
| city | NULL |
| zip_code | NULL |
| sector | NULL |
| phone | NULL |
| website | NULL |
| created_at | NOT NULL |
| updated_at | NOT NULL |

---

## mission
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| **company_id** (FK → company.id) | NOT NULL |
| title | NOT NULL |
| description | NOT NULL |
| city | NOT NULL |
| start_date | NOT NULL |
| end_date | NULL |
| hourly_rate | NULL |
| contract_type | NOT NULL |
| slots | NOT NULL, défaut `1` |
| status | NOT NULL, défaut `draft` |
| created_at | NOT NULL |
| updated_at | NOT NULL |

---

## candidature
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| **worker_id** (FK → worker.id) | NOT NULL |
| **mission_id** (FK → mission.id) | NOT NULL |
| cover_letter | NULL |
| status | NOT NULL, défaut `pending` |
| created_at | NOT NULL |
| updated_at | NOT NULL |
| — | UNIQUE (worker_id, mission_id) |

---

## media
| Colonne | Contrainte |
|---|---|
| **id** (PK) | NOT NULL |
| **worker_id** (FK → worker.id) | NOT NULL, UNIQUE |
| filename | NOT NULL |
| original_name | NOT NULL |
| mime_type | NOT NULL |
| size | NOT NULL |
| type | NOT NULL, défaut `worker_avatar` |
| created_at | NOT NULL |
