erDiagram
    %% Relations
    HOSPITAL ||--o{ BED : "possède"
    SPECIALTY ||--o{ BED : "concerne"
    SPECIALTY_GROUP ||--o{ SPECIALTY : "regroupe"
    HOSPITAL }o--o{ SPECIALTY : "propose"

    %% Tables
    HOSPITAL {
        BIGINT id PK "AUTO"
        VARCHAR name UK "Nom de l'hôpital"
        VARCHAR address "Adresse"
        VARCHAR city "Ville"
        VARCHAR postal_code "Code postal"
        DOUBLE latitude "GPS"
        DOUBLE longitude "GPS"
        VARCHAR phone_number "Téléphone"
        INTEGER total_beds "Nombre total"
        INTEGER available_beds "Lits dispos"
        BOOLEAN is_active "Statut actif"
        TIMESTAMP created_at "Audit"
        TIMESTAMP updated_at "Audit"
    }

    SPECIALTY {
        BIGINT id PK "AUTO"
        VARCHAR code UK "Code NHS"
        VARCHAR name UK "Nom spécialité"
        BIGINT specialty_group_id FK "Groupe parent"
        TEXT description "Détails"
        BOOLEAN is_active "Statut actif"
        TIMESTAMP created_at "Audit"
    }

    SPECIALTY_GROUP {
        BIGINT id PK "AUTO"
        VARCHAR code UK "Code groupe"
        VARCHAR name UK "Nom groupe"
        TEXT description "Détails"
        BOOLEAN is_active "Statut actif"
        TIMESTAMP created_at "Audit"
        TIMESTAMP updated_at "Audit"
    }

    BED {
        BIGINT id PK "AUTO"
        BIGINT hospital_id FK "Réf hôpital"
        BIGINT specialty_id FK "Réf spécialité"
        VARCHAR bed_number "N° de lit"
        VARCHAR room_number "N° de chambre"
        INTEGER floor "Étage"
        VARCHAR status "AVAILABLE, OCCUPIED..."
        BOOLEAN is_available "Disponible?"
        TIMESTAMP last_occupied_at "Audit occupation"
        TIMESTAMP created_at "Audit"
        TIMESTAMP updated_at "Audit"
    }

    HOSPITAL_SPECIALTY {
        BIGINT hospital_id PK "Composite PK"
        BIGINT specialty_id PK "Composite PK"
    }

    APP_USER {
        BIGINT id PK "AUTO"
        VARCHAR username UK "Login"
        VARCHAR password "Hash BCrypt"
        VARCHAR email UK "Contact"
        VARCHAR roles "ROLE_USER,..."
        BOOLEAN is_active "Accès autorisé"
        TIMESTAMP created_at "Audit"
        TIMESTAMP updated_at "Audit"
    }
