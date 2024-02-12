# Article CJS - ESM

# Introduction

## **CommonJS (cjs) :**

- **Origine :** CommonJS est une spécification de module pour JavaScript qui a été développée pour une utilisation côté serveur.
- **Date :** Introduit autour de 2009.
- **Créateurs :** Kevin Dangoor
- **Adoption dans Node.js :** Node.js a adopté CommonJS comme son système de module par défaut dès ses premières versions. Les modules CommonJS utilisent les mots-clés `require` pour importer des modules et `module.exports` pour exporter des fonctionnalités.

## **ECMAScript Modules (ESM) :**

- **Origine :** Les modules ECMAScript (ESM) font partie des spécifications ECMAScript (le standard sur lequel est basé JavaScript). ESM a été introduit dans ECMAScript 6 (ES2015) pour fournir un système de module standardisé pour JavaScript.
- **Date :** Introduit en juin 2015 avec ECMAScript 6 (ES2015).
- **Adoption dans Node.js :** Bien que Node.js ait initialement utilisé CommonJS, il a commencé à prendre en charge les modules ECMAScript avec l'introduction de l'option `-experimental-modules` dans Node.js 8.5. Avec le temps, le support ESM dans Node.js est devenu plus mature et, à partir de Node.js 13, l'utilisation d'ESM est devenue stable sans nécessiter l'option `-experimental-modules`.

## **Comparaison entre CommonJS et ESM :**

- **Syntaxe d'importation :**
    - **CommonJS :** `const module = require('module');`
    - **ESM :** `import module from 'module';`
- **Syntaxe d'exportation :**
    - **CommonJS :** `module.exports = someFunction;`
    - **ESM :** `export default someFunction;`
- **Chargement :**
    - **CommonJS :** Chargement synchrone des modules.
    - **ESM :** Chargement asynchrone des modules.
- **Compatibilité** :
    - **CommonJS : F**onctionne dans Node.js mais pas dans les navigateurs
    - **ESM :** Fonctionne dans la plus-part des navigateurs
- **Portée des modules :**
    - **CommonJS :** Les modules sont toujours exécutés dans le même contexte.
    - **ESM :** Chaque module a sa propre portée, ce qui favorise l'encapsulation.
- **Interoperabilité :**
    - **CommonJS** : Ne peut importer de modules ESM qu’avec la directive `import()`.
    - **ESM** : Peut importer des modules CommonJS sans aucune modification du code.
- **Extension de fichier** :
    - **CommonJS** : `.js` ou `.cjs`. Node.js considère l'extension `.js` par défaut. Par conséquent elle est implicite lorsqu’elle n’est pas présente dans un `require`.
    - **ESM** : `.mjs` . Cette extension est à préciser explicitement.

Bien que CommonJS ait été le système de module dominant dans Node.js, l'adoption croissante d'ESM a été constatée, offrant des avantages tels que la syntaxe plus concise et le chargement asynchrone. Cependant la majorité des projets Node.js sont encore écrit et maintenu en CommonJS.

## **Migration CommonJS vers ESM :**

La migration d'un projet CommonJS (Node.js) vers ECMAScript Modules (ESM) peut présenter plusieurs défis, mais elle peut également offrir des avantages significatifs. Voici quelques-unes des difficultés courantes lors de cette transition, ainsi que les raisons pour lesquelles cette migration peut être bénéfique :

### **Difficultés de migration :**

1. **Syntaxe différente :** ESM utilise une syntaxe d'import/export différente de CommonJS. Cela signifie que tous les fichiers doivent être mis à jour pour utiliser la nouvelle syntaxe.
2. **Charge dynamique :** ESM traite l'importation comme une opération statique, ce qui signifie que les imports dynamiques comme **`require(variable)`** ne sont pas autorisés comme dans CommonJS.
3. **Résolution des chemins :** ESM a des règles de résolution de chemin différentes par rapport à CommonJS. Les chemins absolus et relatifs peuvent nécessiter des ajustements.
4. **Interopérabilité :** Les modules ESM ne peuvent pas être importés directement dans des fichiers CommonJS sans certaines configurations spécifiques.
5. **Support de modules tiers :** Certains modules tiers peuvent ne pas être encore compatibles avec ESM, et il peut être nécessaire d'attendre des mises à jour ou de rechercher des alternatives.
6. **Configuration du projet :** La configuration du projet peut nécessiter des ajustements, notamment pour définir le type de module dans le fichier de configuration (par exemple, **`"type": "module"`** dans le fichier **`package.json`**).

### Exemple de migration :

Chez Ekino nous avons réalisé sur l'un de nos projets open source https://github.com/ekino/node-logger, une migration visant à fournir deux versions compatibles en CommonJS et en ESM. Cette tâche n'a pas été exempte de défis.

- Lien de la PR : https://github.com/ekino/node-logger/pull/46.
- [Explications détaillés](https://github.com/Maugun/node-logger/blob/transpilation-cjs-and-esm-2/ts_to_cjs_and_esm.md) sur le fork de Maugun.

### **Avantages de la migration :**

1. **Performance :** ESM offre des performances potentiellement meilleures en raison de sa nature statique d'importation, permettant aux moteurs JavaScript d'effectuer des optimisations plus efficaces. Cependant, à ce niveau là, l’avantage de l’utilisation des modules ESM se révèle plus intéressant en front qu’en back.
2. **Meilleure statique :** La vérification statique des imports permet de détecter plus facilement les erreurs de dépendances lors de la construction, plutôt qu'à l'exécution.
3. **Meilleure normalisation :** ESM fait partie de la norme ECMAScript, ce qui signifie que l'adoption de cette norme peut rendre le code plus portable et faciliter l'interopérabilité avec d'autres environnements JavaScript.
4. **Futur-proofing :** ESM est la norme future pour JavaScript, et l'industrie tend à adopter cette approche. Migrer vers ESM garantit une meilleure compatibilité avec les évolutions à venir du langage.
5. **Modules réutilisables :** Les modules ESM peuvent être plus facilement réutilisés dans des environnements front-end et d'autres outils de build, favorisant une approche de code partagé entre le côté client et le côté serveur.

En résumé, bien que la migration de CommonJS vers ESM puisse présenter des défis initiaux, elle offre des avantages significatifs en termes de performances, de normalisation et de préparation pour l'avenir de JavaScript. Les équipes de développement doivent évaluer ces avantages par rapport aux efforts nécessaires pour déterminer si la migration est justifiée pour leur projet spécifique.