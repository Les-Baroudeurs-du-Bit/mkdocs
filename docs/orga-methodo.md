# Organisation du Projet et Méthodologie

## Gestion de projet et Organisation du travail (Jira & Versionnage)
Pour structurer notre charge de travail, suivre l'avancement des fonctionnalités et assurer une visibilité claire sur le projet, nous avons fait le choix d'utiliser Jira couplé à une gestion rigoureuse du versionnage (Git / GitHub).

## Pourquoi l'utilisation de Jira ?
Centralisation et Suivi des Tâches : Jira permet de décomposer le projet en Epics, User Stories et Tâches techniques. Chaque fonctionnalité est ainsi tracée de sa conception à sa validation finale.  
Grâce aux tableaux de bord (Kanban / Scrum), l'équipe peut visualiser en temps réel les tâches à faire, en cours (In Progress), en cours de test (In Review) et terminées (Done). De plus, l'utilisation de Jira se combine naturellement avec notre stratégie de branches Git. Chaque commit ou Pull Request peut être relié à un ticket Jira (ex: PROJ-123), ce qui permet de lier directement le code produit à la spécification fonctionnelle ou technique correspondante.

## Priorisation des Fonctionnalités
Pour optimiser notre temps de développement et garantir la livraison d'un produit fonctionnel et stable, la priorisation des fonctionnalités a été réalisée selon une approche agile :
<ul>
    <li>Le Backlog Produit : Toutes les idées, besoins et exigences ont été recensés sous forme d'User Stories dans Jira.</li>
    <li>La Hiérarchisation : Nous avons classé les tâches selon leur criticité (par exemple via la méthode MoSCoW : Must have, Should have, Could have, Won't have pour cette version) :</li>
    <ul>
        <li>Fonctionnalités Clés (Must have) : Le cœur de l'application (socle technique, authentification, fonctionnalités métiers principales).</li>
        <li>Améliorations (Should/Could have) : Fonctionnalités secondaires, optimisations d'interface ou de performance ajoutées une fois le socle stabilisé.</li>
    </ul>
</ul>

## Rôles et Responsabilités : Le Product Owner (PO)
La clarté des rôles est essentielle pour éviter les blocages décisionnels.

### Rôle du Product Owner :  
Il est le garant de la vision du produit et des besoins des utilisateurs/parties prenantes. Il rédige et priorise le Product Backlog dans Jira. Il valide les livrables à la fin de chaque itération pour s'assurer qu'ils répondent aux critères d'acceptation définis.  

Reia a exercé ce rôle tout au long du projet, servant d'intermédiaire pour clarifier les spécifications et valider les choix fonctionnels.

## Processus de Revue de Code (Code Review)
Afin d'assurer la qualité du code source, de prévenir les bugs en amont et de partager la connaissance technique au sein de l'équipe, un processus strict de revue de code a été mis en place :
<ul>
    <li>Workflow Git : Aucun code n'est poussé directement sur la branche principale (main ou master). Chaque développeur travaille sur une branche dédiée.</li>
    <li>Pull / Merge Requests : Une fois la fonctionnalité développée et testée localement, une demande de fusion (Pull Request) est ouverte sur GitHub.</li>
    <li>Validation croisée :</li>
    <ul>
        <li>La Pull Request doit être impérativement relue et validée par au moins un autre membre de l'équipe avant d'être fusionnée.</li>
        <li>Les critères de validation incluent : le respect des conventions de code, l'absence de régression, la lisibilité et l'application des bonnes pratiques de sécurité.</li>
    </ul>
    <li>Automatisation : Nos pipelines d'intégration continue (CI/CD) complètent cette revue humaine par des analyses automatiques de qualité et de sécurité avant chaque fusion.</li>
</ul>

## Explication et Justification des Choix Techniques
Chaque choix technologique (frameworks, bases de données, architectures, outils de CI/CD) réalisé dans ce projet a été mûrement réfléchi pour répondre à des contraintes de performance, de maintenabilité et de compétences de l'équipe :

- Traçabilité : Les grandes décisions d'architecture ou de conception ont été documentées (via des notes de cadrage, des schémas d'architecture ou directement dans le dépôt).

- Adéquation Besoin / Technologie : Les technologies choisies l'ont été pour leur robustesse, leur écosystème documenté et leur pertinence face aux objectifs fixés.