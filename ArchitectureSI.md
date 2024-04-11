
## Modélisation de l'Architecture d'un SI Hôpital


**Diagramme de Flux de Données (DFD)**

```mermaid
graph TD
A[Dossiers Médicaux] --> B[Système de Gestion des Dossiers Médicaux]
B --> C[Base de Données des Dossiers Médicaux]
D[Patients] --> E[Système de Gestion des Patients]
E --> C
F[Personnel Médical] --> G[Système de Gestion du Personnel]
G --> C
H[Laboratoire] --> I[Système de Gestion des Résultats de Laboratoire]
I --> C
J[Pharmacie] --> K[Système de Gestion des Médicaments]
K --> C
C --> L[Système de Facturation]
L --> M[Système de Paiement]
```

**Explication du DFD**

Ce diagramme de flux de données simplifié représente les flux d'informations principaux dans un système d'information hospitalier (SIH). Les entités externes (acteurs) et les systèmes internes sont représentés par des rectangles. Les flèches indiquent le flux des données entre les entités.

* **Dossiers Médicaux:** Stockent les informations médicales des patients.
* **Système de Gestion des Dossiers Médicaux:** Gère et consulte les dossiers médicaux.
* **Base de Données des Dossiers Médicaux:** Stocke les données des dossiers médicaux.
* **Patients:** Fournissent des informations personnelles et médicales.
* **Système de Gestion des Patients:** Gère les informations des patients et planifie les rendez-vous.
* **Personnel Médical:** Accède et met à jour les dossiers médicaux et prescrit des traitements.
* **Système de Gestion du Personnel:** Gère les informations du personnel médical et planifie les horaires.
* **Laboratoire:** Effectue des analyses et transmet les résultats.
* **Système de Gestion des Résultats de Laboratoire:** Gère et consulte les résultats de laboratoire.
* **Pharmacie:** Fournit des médicaments et gère les stocks.
* **Système de Gestion des Médicaments:** Gère les stocks de médicaments et les ordonnances.
* **Système de Facturation:** Génère les factures pour les services médicaux.
* **Système de Paiement:** Traite les paiements des patients.

Ce DFD fournit une vue d'ensemble simplifiée des flux de données dans un SIH. Des diagrammes plus détaillés peuvent être créés pour chaque sous-système, illustrant les interactions internes et les processus spécifiques.

**Diagramme de Classes UML**

```mermaid
classDiagram
    Patient "1" -- "0..*" Dossier : a
    Dossier "1" -- "0..*" Consultation : contient
    Dossier "1" -- "0..*" Analyse : contient
    Dossier "1" -- "0..*" Prescription : contient
    Consultation "1" -- "1" Medecin : consulté par
    Prescription "1" -- "1" Medecin : prescrit par
    Prescription "1" -- "1" Medicament : concerne
    Dossier "1" -- "0..*" Facture : génère
    Facture "1" -- "1..*" Paiement : est réglée par
    Dossier "1" -- "0..*" Hospitalisation : inclut
    Hospitalisation "1" -- "1" Chambre : utilise

    class Patient{
      +int id
      +String nom
      +String prenom
      +Date dateNaissance
      +String adresse
      +String numeroSecuriteSociale
      +Dossier[] dossiersMedicaux
    }

    class Dossier{
      +int id
      +Patient patient
      +Date dateOuverture
      +Date dateFermeture
      +Consultation[] historiqueConsultations
      +Analyse[] historiqueAnalyses
      +Prescription[] historiquePrescriptions
      +Facture[] factures
      +Hospitalisation[] hospitalisations
    }

    class Consultation{
      +int id
      +Dossier dossier
      +Date dateConsultation
      +Medecin medecin
      +String diagnostic
      +String traitement
    }

    class Medecin{
      +int id
      +String nom
      +String prenom
      +String specialite
      +Consultation[] consultations
    }

    class Analyse{
      +int id
      +Dossier dossier
      +Date dateAnalyse
      +String typeAnalyse
      +String resultat
    }

    class Prescription{
      +int id
      +Dossier dossier
      +Date datePrescription
      +Medecin medecin
      +Medicament medicament
      +int quantite
      +String posologie
    }

    class Medicament{
      +int id
      +String nom
      +String[] principesActifs
      +String indication
      +String[] contreIndications
    }

    class Facture{
      +int id
      +Dossier dossier
      +Date dateEmission
      +float montantTotal
      +String statut
      +Paiement[] paiements
    }

    class Paiement{
      +int id
      +Facture facture
      +Date datePaiement
      +float montant
      +String modePaiement
    }

    class Hospitalisation{
      +int id
      +Dossier dossier
      +Date dateDebut
      +Date dateFin
      +Chambre chambre
      +String motif
    }

    class Chambre{
      +int id
      +String numero
      +String type
      +float tarifParNuit
    }

```
