# Choix des modèles d'IA

## Objectif

Au cours du projet, nous avons utilisé plusieurs IA pour des tâches très différentes : génération de maquettes, story mapping, reformulation de textes, développement du squelette PWA... Cette page cherche à déterminer, pour chacune de ces tâches, le modèle le plus adapté selon le rapport **qualité de la réponse / coût**, en euros comme en tokens.

## Source et limites

Nous nous appuyons sur le classement [CursorBench 4.0](https://cursor.com/cursorbench), qui évalue des agents IA sur des tâches de développement ambiguës et multi-fichiers issues de vraies sessions Cursor. Le coût par tâche y est calculé à partir des tarifs publics de chaque modèle.

Quelques limites à garder en tête :

- CursorBench ne mesure **que des tâches de code**. Pour les tâches non techniques (maquette, user stories, rédaction), nos recommandations sont des extrapolations.
- Selon Cursor, des écarts de l'ordre d'un point de score ne sont pas statistiquement significatifs.
- Les modèles Gemini que nous avons utilisés (Gemini Pro, Gemini Flash) n'apparaissent pas sous ce nom dans le classement : ils ne sont donc pas comparés directement.
- Cette analyse a été réalisée avec l'aide de Claude (Anthropic), ce qui peut introduire un biais en faveur des modèles Claude.
- Conversion utilisée : 1 $ ≈ 0,86 € (taux approximatif).

## Les meilleurs compromis qualité / coût

Le tableau ci-dessous ne retient que les configurations qu'aucune autre ne bat à la fois en score et en prix.

| Configuration             | Score      | Coût / tâche | ≈ €        | Tokens / tâche | Étapes / tâche |
| ------------------------- | ---------- | ------------ | ---------- | -------------- | -------------- |
| Haiku 5.5 Low             | 30,9 %     | 0,08 $       | 0,07 €     | 23 k           | 25             |
| Haiku 5.5 Medium          | 36,9 %     | 0,17 $       | 0,15 €     | 43 k           | 39             |
| Haiku 5.5 High            | 42,3 %     | 0,32 $       | 0,28 €     | 77 k           | 59             |
| Haiku 5.5 Extra High      | 44,3 %     | 0,56 $       | 0,48 €     | 144 k          | 93             |
| Haiku 5.5 Max             | 48,4 %     | 1,12 $       | 0,96 €     | 326 k          | 163            |
| **Sonnet 5.5 Extra High** | **53,1 %** | **2,81 $**   | **2,42 €** | 100 k          | 78             |
| **Opus 5.5 High**         | **56,0 %** | **3,97 $**   | **3,41 €** | 53 k           | 68             |
| Opus 5.5 Max              | 57,8 %     | 13,43 $      | 11,55 €    | 218 k          | 185            |

### Ce qu'on en retient

- **Pour coder au meilleur prix : Haiku 5.5 High ou Extra High.** Il atteint environ 80 % du score d'Opus pour 8 à 14 % de son coût.
- **Pour coder avec une bonne qualité : Opus 5.5 High.** Il obtient le même score qu'Opus 5.5 Extra High pour deux fois moins cher, et fait mieux que Sonnet 5.5 Max et que toutes les configurations de Fable 5.1.
- **Fable 5.1 n'est pas rentable pour une SAE** : en High, il obtient 49,2 % pour 9,08 dollars alors qu'Haiku 5.5 Max fait presque aussi bien pour 1,12 dollars.
- **Coût en euros et coût en tokens ne vont pas toujours ensemble.** Haiku 5.5 Max consomme six fois plus de tokens qu'Opus 5.5 High (326 k contre 53 k), mais coûte 3,5 fois moins cher. Le nombre de tokens pèse sur les quotas, la fenêtre de contexte et le temps d'attente ; le prix en euros pèse sur le budget.

### Tarifs publics des modèles Claude (par million de tokens)

| Modèle     | Entrée | Sortie |
| ---------- | ------ | ------ |
| Haiku 5.5  | 0,10 $ | 0,50 $ |
| Sonnet 5.5 | 2 $    | 10 $   |
| Opus 5.5   | 4 $    | 20 $   |
| Fable 5.1  | 10 $   | 50 $   |

## Critères complémentaires

En plus du rapport qualité / coût, nous avons retenu les critères suivants :

- **Nombre d'étapes par tâche** : un bon indicateur du temps d'attente réel.
- **Efficacité en tokens** : importante en cas de quotas ou d'abonnement plafonné.
- **Lecture d'images** : nécessaire pour transmettre une photo du story mapping ou une capture de maquette.
- **Recherche web** : indispensable pour les comparatifs de technologies et l'étude de l'existant.
- **RGPD et lieu de traitement des données** : cohérent avec notre page RGPD. Certains modèles bien placés en coût (DeepSeek, par exemple) posent question sur l'hébergement des données.
- **Offres gratuites pour étudiants** : un modèle gratuit reste imbattable en rapport qualité / prix, ce qui explique en partie notre usage de Gemini Pro.

## Recommandation par tâche

| Tâche                                                | Modèle conseillé                                                                                     | Justification                                                                                                                                                                                                                                                                 |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Maquette avec Figma Make**                         | Le modèle est imposé par l'outil. Rédiger le prompt avec **Haiku 5.5 Medium** ou **Sonnet 5.5 Low**. | Le vrai levier est le prompt. Notre suivi des tokens le montre : un prompt vague a coûté 30 000 + 50 000 tokens pour un résultat hors sujet, un prompt détaillé 30 000 tokens pour un bon résultat. Rédiger un prompt est une tâche de reformulation, un petit modèle suffit. |
| **Refonte complète de la maquette en code**          | **Sonnet 5.5 Extra High**, ou **Opus 5.5 High** si la fidélité au design est prioritaire             | CursorBench 4.0 évalue justement le respect du design. Sonnet coûte deux fois moins cher par token qu'Opus.                                                                                                                                                                   |
| **User stories et story mapping**                    | **Sonnet 5.5 Medium**, ou **Haiku 5.5 High**                                                         | La tâche demande du raisonnement produit mais les réponses sont courtes. Les deux modèles savent lire une photo du tableau.                                                                                                                                                   |
| **Reformulation de textes du mkdocs**                | **Haiku 5.5 Low ou Medium**                                                                          | Une reformulation (environ 2 000 tokens en entrée, 1 000 en sortie) coûte environ 0,0007 $ avec Haiku contre 0,03 $ avec Opus, pour une qualité quasi identique.                                                                                                              |
| **Squelette PWA, cas limites, refactorisation**      | **Haiku 5.5 Extra High** pour itérer, **Opus 5.5 High** pour la refactorisation finale               | C'est exactement le type de tâche mesuré par CursorBench.                                                                                                                                                                                                                     |
| **Aide SSH / MariaDB**                               | **Haiku 5.5 Medium**                                                                                 | Questions classiques et très bien documentées.                                                                                                                                                                                                                                |
| **Recherche (applications existantes, comparatifs)** | **Sonnet 5.5 Medium avec recherche web**, ou Gemini Flash                                            | La qualité dépend surtout des sources trouvées, pas du modèle.                                                                                                                                                                                                                |
| **Rédaction de la page RGPD**                        | **Sonnet 5.5 Medium**, suivi d'une relecture humaine                                                 | Une erreur dans un texte juridique coûte cher : un modèle intermédiaire suffit, mais la relecture reste indispensable.                                                                                                                                                        |

## Bilan sur notre consommation

La ligne **Claude Code Opus 5.5 : 25 000 000 tokens** de notre suivi représente à elle seule plus de 99 % de nos tokens. Son coût dépend surtout du cache : environ 5 dollars si la majorité des tokens sont relus depuis le cache (0,20 dollars par million), jusqu'à environ 100 dollars s'ils sont tous facturés comme nouvelle entrée (4 dollars par million). Avec Sonnet 5.5, le coût par token aurait été divisé par deux environ.

## Conclusion

La règle que nous retenons : **un petit modèle pour le texte, un modèle intermédiaire pour la réflexion produit, un gros modèle uniquement pour le code complexe, et des prompts précis dans tous les cas.**
