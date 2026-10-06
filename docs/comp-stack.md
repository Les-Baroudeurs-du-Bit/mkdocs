

# Analyse détaillée des technologies
## Synthèse de la Stack
```
[ Frontend PWA ]           Vue.js (Vite + Pinia) + Leaflet (Cartes)
        │  
        ▼ (REST / JSON + JWT)
[ Backend API ]            Spring Boot (Java 17/21) + Spring Security
         │
        ▼ (JDBC / JPA Hibernate)
[ Base de Données ]      MySQL 8.0 sur MariaDB
         │
[ Infrastructure ]             Docker (Conteneurisation) + GitLab CI/CD
```
Cette combinaison allie la rapidité d'exécution front-end (Vue.js pour une PWA réactive et simple à mettre en cache hors-ligne) à la rigueur logicielle back-end (Spring Boot et MySQL pour la robustesse des données et l'application stricte des Design Patterns).

## Justification
### Frontend : Vue.js vs React.js
| Critères  | Vue.js (avec Vite) | React.js (avec Vite / Next.js) |
| -: | :- | :- |
| **Intégration PWA & Offline** | **Excellent :** L'outillage (vite-plugin-pwa) est fluide et génère le Service Worker et le manifeste avec une configuration minimale. | **Très bonne :** Nécessite souvent un peu plus de configuration manuelle ou des dépendances tierces (ex: Workbox configuré sur-mesure). |
| **Courbe d'apprentissage & Vélocité Agile** | **Rapide :** La séparation claire template/script/style (Single File Components) facilite la répartition des tâches au sein d'une équipe. | **Moyenne :** Le paradigme JSX et la gestion fine des re-renders demandent une rigueur accrue pour éviter les fuites de performances. |
| **Gestion d'état global (Offline cache)** | **Très fluide :** Pinia offre une gestion de store typée, intuitive et facilement synchronisable avec IndexedDB. | **Très robuste :** Redux Toolkit ou TanStack Query sont puissants mais introduisent du code boilerplate plus lourd. |

**Le verdict pour le projet : Vue.js**  
Pourquoi ? Pour un projet où les délais sont rythmés par des sprints agiles, Vue.js offre un ratio vélocité/qualité optimal. Son écosystème avec Vite permet de configurer le mode hors-ligne (Service Worker + mise en cache des cartes et plannings) sans complexité accidentelle, tout en garantissant un code propre et maintenable.

### Backend : Java Spring Boot vs Node.js & Express.js
| Critères | Spring Boot (Java) | Node.js (Express.js) |
| -: | :- | :- |
| **Architecture & Bonnes Pratiques** | **Très structurée :** Impose naturellement une architecture en couches (Controller, Service, Repository, DTO), des interfaces et l'injection de dépendances. | **Très libre :** Flexible, mais le manque de cadre strict peut mener à du code spaghetti ou à des disparités de style selon les développeurs. |
| Typage & Fiabilité | **Typage fort (Java) :** Détecte la majorité des erreurs à la compilation, idéal pour sécuriser les calculs financiers (budget/caisse commune). | **Faible (JavaScript) :** à moins d'utiliser TypeScript. Les erreurs d'inattention peuvent survenir au moment de l'exécution. |
| **Homogénéité de la Stack** | Deux langages différents entre front et back (Java et JS/TS), demandant de la polyvalence. | Stack 100% JavaScript/TypeScript de bout en bout (partage potentiel de types et validation de schémas). |
| **Performance & I/O** | Modèle multithread robuste, un peu plus lourd au démarrage et en mémoire. | Modèle asynchrone non-bloquant (Event Loop), très léger et idéal pour le streaming de médias ou les websockets. |


**Le verdict pour le projet : Spring Boot**  
Pourquoi ? Le cahier des charges insiste sur la qualité du code et les bonnes pratiques d'ingénierie logicielle. Spring Boot impose un cadre industriel rigoureux (séparation nette des responsabilités, gestion stricte des entités pour le budget et la sécurité via Spring Security / JWT). C'est le choix le plus convaincant pour démontrer la maîtrise d'un cycle de développement logiciel complet.

### Base de données : MySQL (SQL) vs MongoDB (NoSQL)
| Critères | MySQL | MongoDB |
| -: | :- | :- |
| **Cohérence des données (Transactions ACID)** | **Totale :** Gestion irréprochable des clés étrangères, intégrité référentielle native. | **Éventuelle :** Moins adapté nativement aux calculs de dettes croisées complexes entre membres d'un groupe. |
| **Flexibilité des étapes du Road Trip** | **Rigide :** Une étape avec hôtel, une étape avec visite et une étape "trajet" nécessitent soit plusieurs tables reliées, soit des colonnes nullables. | **Maximale :** Chaque document d'étape peut avoir son propre schéma (notes libres, checklists, coordonnées, URLs d'images). |
| **Modélisation du voyage** | Nécessite des tables d'association (Utilisateurs←→Voyages ←→ Étapes ←→Dépenses). | Stocke un voyage complet sous forme de document JSON hiérarchique, très facile à requêter et à cacher en local. |

**Le verdict pour le projet : MySQL**  
Pourquoi ? Même si MongoDB séduit par sa souplesse pour les étapes, l'application comporte des relations fortes et critiques : gestion des rôles (qui a le droit de modifier le road trip), caisse commune (qui doit quoi à qui), et liste des amis notifiés pour les selfies. Une base relationnelle avec des contraintes d'intégrité strictes évite les incohérences de données, notamment lors des synchronisations hors-ligne où deux utilisateurs pourraient modifier des plannings simultanément.

### API de Géolocalisation & Cartographie : Mapbox vs OpenStreetMap (Nominatim)
| Critères | Mapbox API | OpenStreetMap (Nominatim / Leaflet) |
| -: | :- | :- |
| **Reverse Geocoding (Coordonnées $\rightarrow$ Nom de lieu)** | **Très précis et rapide :** Retourne des noms de lieux clairs et touristiques (ex: Château de Neuschwanstein). | **Variable :** Dépend des contributions communautaires, parfois verbeux ou imprécis selon les zones rurales. |
| **Coût & Quotas** | Modèle freemium (généreux au début, mais carte bancaire et facturation au-delà des quotas). | **100% gratuit et Open Source :** Idéal pour un projet universitaire, mais soumis à une limite stricte de débit (1 requête/seconde max pour Nominatim). |
| **Rendu cartographique PWA** | SDK vectoriel très fluide et interactif, rendu esthétique sur mobile et PC. | Excellente intégration avec la librairie Leaflet.js, très légère pour une PWA mobile. |

**Le verdict pour le projet : OpenStreetMap (Leaflet + Nominatim)**  
Pourquoi ? Dans le cadre d'une SAE, privilégier une solution open source sans risque de dépassement de facturation est un choix responsable. Pour la fonctionnalité du selfie quotidien (une requête par jour par voyageur), la limite de débit de Nominatim n'est absolument pas un problème, et la légèreté de la bibliothèque Leaflet sur mobile garantit une excellente fluidité dans la PWA.
