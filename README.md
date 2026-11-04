# Évaluation Pratique : Intégration Hibernate & JPA avec Architecture Microservices

**Réalisé par :** Zakaria Laalyej (2DSI)  
**Module :** JEE / Architecture Microservices : Conception, Déploiement et Orchestration  

Cette évaluation regroupe trois cas concrets d'architecture métier modélisés avec **JPA**, **Hibernate** et le patron de conception **DAO / Service** :
1. **Exercice 1 : Gestion de stock** pour un magasin de produits informatiques.
2. **Exercice 2 : Gestion de projets** pour le suivi des temps et des coûts par un bureau d'études.
3. **Exercice 3 : Gestion de l'état civil** pour l'administration des citoyens et de leurs relations matrimoniales.

---

## Objectifs

- Maîtriser le mapping objet-relationnel complexe (héritage `JOINED`, associations `@ManyToOne`, `@OneToMany`, entités d'association avec clés composées `@EmbeddedId`).
- Développer des services métier avec l'interface générique `IDao<T>`.
- Formuler des requêtes avancées : requêtes JPQL/HQL nommées (`@NamedQuery`), requêtes SQL natives nommées (`@NamedNativeQuery`) et requêtes programmatiques via **JPA Criteria API**.
- Valider les opérations avec des scénarios de test complets et un affichage en console structuré.

---

## Technologies Utilisées

- **Java 17 / 21**
- **Hibernate 5.6 / JPA 2.2**
- **H2 Database (en mémoire) / MySQL ready**
- **JUnit 4**
- **Maven**

---

## Architecture des Trois Exercices

```
evaluation-microservices/
├── pom.xml
├── README.md
├── captures/
└── src/
    ├── main/
    │   ├── java/ma/projet/
    │   │   ├── dao/IDao.java                   # Interface DAO générique
    │   │   ├── util/HibernateUtil.java         # Gestionnaire de SessionFactory
    │   │   │
    │   │   │── [Exercice 1 - Gestion de Stock]
    │   │   ├── classes/ (Categorie, Produit, Commande, LigneCommandeProduit)
    │   │   ├── service/ (CategorieService, ProduitService, CommandeService, LigneCommandeService)
    │   │   ├── test/TestStock.java
    │   │   │
    │   │   │── [Exercice 2 - Gestion de Projets]
    │   │   ├── classes/ (Employe, Projet, Tache, EmployeTache)
    │   │   ├── service/ (EmployeService, ProjetService, TacheService, EmployeTacheService)
    │   │   ├── test/TestProjets.java
    │   │   │
    │   │   │── [Exercice 3 - État Civil]
    │   │   ├── beans/ (Personne, Homme, Femme, Mariage)
    │   │   ├── service/ (HommeService, FemmeService, MariageService)
    │   │   ├── test/TestEtatCivil.java
    │   │   │
    │   │   └── App.java                        # Démonstration globale des 3 modules
    │   └── resources/META-INF/persistence.xml
    └── test/java/ma/projet/AppTest.java
```

---

## Fonctionnalités Clés Implémentées

### Exercice 1 : Gestion de Stock
- Produits par catégorie.
- Produits commandés entre deux dates données.
- Produits commandés dans une commande donnée avec calcul des sous-totaux.
- Requête nommée : Produits dont le prix est strictement supérieur à 100 DH.

### Exercice 2 : Gestion de Projets
- Suivi des tâches planifiées vs réalisées (dates réelles).
- Tâches réalisées par un employé et projets sous sa direction.
- Requête nommée : Tâches dont le montant dépasse 1000 DH.
- Tâches réalisées entre deux dates.

### Exercice 3 : Gestion de l'État Civil
- Suivi matrimonial complet (mariages en cours vs mariages échoués).
- Requête native nommée : Nombre d'enfants d'une femme entre deux dates.
- Requête nommée JPQL : Femmes mariées au moins deux fois.
- **Criteria API JPA** : Nombre d'hommes mariés à quatre femmes simultanément entre deux dates.
- Jeu d'essai de validation avec 10 femmes et 5 hommes.

---

## Exécution des Tests

```bash
# Compiler et lancer la démonstration globale
mvn clean compile exec:java -Dexec.mainClass="ma.projet.App"

# Lancer la suite de tests unitaires
mvn test
```

---

## Captures d'Écran

> Déposez vos captures d'écran dans le dossier `captures/` :
> - `captures/01-test-stock.png` : Sortie console de la gestion de stock.
<img width="799" height="601" alt="image" src="https://github.com/user-attachments/assets/a12d5f96-2f80-4daf-afdc-36e73dfed003" />

> - `captures/02-test-projets.png` : Sortie console du suivi des projets et tâches réelles.
<img width="999" height="571" alt="image" src="https://github.com/user-attachments/assets/766bbbbb-782b-4d3f-bb77-f3067b4d8823" />

> - `captures/03-test-etat-civil.png` : Sortie console de l'état civil (mariages en cours, polygamie via Criteria).
<img width="1060" height="591" alt="image" src="https://github.com/user-attachments/assets/28bb2ef5-9f1d-48f1-8e22-1ff89a8766a8" />
<img width="1258" height="646" alt="image" src="https://github.com/user-attachments/assets/e2774517-adc0-480f-91df-f3cd90a74fd9" />

