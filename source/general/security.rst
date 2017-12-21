########
Sécurité
########

Cette page décrit quelques une des "meilleurs pratiques" au niveau de la sécurité web et des détails sur les fonctionnalités de sécurité interne de CodeIgniter.

.. Note :: Si vous êtes venu à la recherche d'un contact à propos de la sécurité, veuillez vous référer au Guide de Contribution. <../contributing/index>`.

Sécurité des URI
=============================

CodeIgniter est plutôt restrictif par rapport aux caractères qu'il autorise dans les chaînes d'URI. Afin de minimiser la possibilité que ds données malveillantes puissent être transmises à votre application. Les URIs ne peuvent contenir que les éléments suivants : 
-  Texte Alpha-Numériques (caractères latins uniquement)
-  Tilde: ~
-  Signe de pourcentage : %
-  Point à la ligne: .
-  Deux-points: :
-  Underscore : \_
-  Tiret: -
-  Espace

Register_globals
================

Durant l'initialisation du système, les variables globales qui existe dans les tableaux  ``$_GET``, ``$_POST``, ``$_REQUEST`` and ``$_COOKIE`` sont supprimées.

La routine de suppression est en fait la même que *register_globals = off*.

display_errors
==============

Dans l'environnement de production, il est généralement souhaitable de "désactiver" les rapports d'erreur de PHP en définissant l'indicateur interne "display_errors" à 0. Cela empêche les erreurs PHP natives d'être affichés, ce qui pourrait afficher des informations sensibles.

Paramétrer la constante **ENVIRONMENT** de CodeIngiter dans index.php à la valeur de 
**\'production\'** n'affichera plus ces erreurs. en mode développement, il est recommandée d'utilisé la valeur 'development'. Plus d'information peuvent être trouvée sur les différences entre les différents environnements sur 
:doc: `Handling Environments <environments>` page.

magic_quotes_runtime
====================

La directive *magic_quotes_runtime* sont désactivés pensant l'initialisation du système donc vous n'avez pas à enlevé les slashes quand vous récupérer des données depuis la base de données.

*************************
Bonne pratiques.
*************************

Avant d'importer une donnée dans votre application, qu'elle soit soumise avec POST lors de la soumission d'un formulaire, qu'elle vienne d'un cookie, d'une URI, d'un fichier XML ou même du tableau "SERVER", vous êtes encouragés à utilisé ces 3 étapes d'approches :

#. Validez les données pour vous assurer qu'elles soient conforme au type, à la longueur, à la taille .
#. Filtrer les données comme si elles étaient corrompues.
#. Échapper les données avant de les soumettre dans votre base de données ou de les transmettre à un navigateur.

CodeIgniter fournit les fonctions et conseils suivant pour vous aider dans ce processus :

XSS Filtering
=============

CodeIgniter viens avec un filtre "Cross Site Scripting". Ce filtre recherche les techniques couramment utilisées pour intégrer du JavaScript malveillant dans vos donnée :doc:` le filtre est décrit ici <../libraries/security>`.

.. note:: Le filtrage XSS devrait *n'être effectué qu'en sortie*. Le filtrage des données d'entrée peut modifier les données de manière indésirable, en enlevant des caractères spéciaux des mots de passes, ce qui peut réduire la sécurité au lieu de l'améliorer.

CSRF protection
===============

CSRF veut dire "Cross-Site Request Forgery", Qui est le processus par lequel un attaquant piège sa victime en l'obligeant à soumettre une requête sans le savoir.

CodeIgniter offre une protection CRSF toute prête, qui se déclenche automatiquement pour chaque requête HTTP qui n'est pas en GET, mais vous impose également de créer vos formulaires de soumission d'une certaine façon. Tout est expliqué dans la  :doc:` Documentation de la librairies de sécurité <../libraries/security>`.

Gestion des mots de passe
============================

Il est *très important* que vous gériez les mots de passes de manière correcte dans votre application.

Malheureusement, beaucoup de développeurs ne savent pas comment faire ça, et le web est rempli de conseils obsolète ou mauvais, ce qui n'aide pas vraiment.

Nous aimerions vous donner une liste de "faire et ne pas faire" pour vous aider avec tout ça :

-  NE STOCKER PAS les mots de passe en texte brut

   Toujours **crypter (hash)** vos mots de passe.

-  N'UTILISER PAS le Base64 ou d'autre encodage similaire pour stocker vos mots de passe.

   Ça reviens à les stocker en texte brut, **hacher**,
   pas *encoder*.

   Encoder et hachage sont des processus bidirectionnels. Les mots de passe sont secret et doivent être uniquement connus de leurs propriétaire et ne doivent marcher que dans une seule direction.
-  N'UTILISER PAS des algorithmes de hachage faible ou qui ont déjà été cassé comme le MD5 ou le SHA1.
   Ces algorithmes sont vieux, ont prouvés qu'ils était défectueux et n'ont pas été pensée pour le cryptage de mot de passe en premier lieux.

  Aussi, N'INVENTER PAS vos propres algorithmes.

   N'utilisez que des algorithmes de hachage de mot fort, tel que BCrypt, qui est utiliser dans les fonctions de hachage de mot de passe de PHP.

Utilisez ces algorithmes s'il vous plait, même si votre version de php n'est pas PHP5.5 ou plus, CodeIgniter vous les fournit.

N'ENVOYEZ ou N'AFFICHEZ jamais votre mot de passe au format texte.

Même pour le propriétaire du mot de passe, si vous avez besoin d'une fonctionnalité "Mot de passe oublié, générez simplement une seul fois un nouveau mot de passe (une seul fois, c'est important) et envoyer le à la place.

N'IMPOSER pas de limites inutiles sur les mots de passe de vos utilisateurs

Si vous utilisez un algorithme de hachage autre que BCrypt (qui à une limite de 72 caractères), vous devriez définir une limite relativement haute dans la taille des passwords pour atténuer les attaques DOS (Deny of Service - Attaque par déni de service), disons 1024 caractères.

A part cela, il ne sert cependant à rien de forcer des règles de limite dans la limite de caractères du mot de passe ou d’empêcher certain caractères spéciaux.


   Non seulement ça **réduit**  la sécurité au lieu de l'améliorer,
 mais il n'y a littéralement aucune raison de le faire.
Aucune limite technique et aucune contrainte de stockage (pratique) ne s'appliquent une fois que vous les avez hachées, aucune ! 


Valider les données en entrée
===================================

CodeIgniter a une :doc: `Librarie de validation de formulaires../libraries/form_validation>` Qui vous assiste pour valider, filtrer et préparer vos données.

Même si cela ne fonctionne pas pour votre cas d'utilisation, soyez sur de toujours valider et désinfecter vos données d'entrée. Par exemple, si vous vous attendiez à avoir une chaîne numérique dans une variable, vous pouvez vérifier cela avec la fonction  ``is_numeric()``
ou ``ctype_digit()``.
Essayer toujours de faire vos vérifications en suivant un certain patron.

Garder en tête que cela n'inclue pas que les superVariables $_POST et $_GET, mais aussi les cookies, les données de l'utilisateur, et plus généralement toutes les données qui ne sont pas créer directement par notre propre code.


Échapper toutes les données avant insertion dans la base de données.
=========================================================================================

N'insérer jamais d'information dans votre base de données sans les échapper. Regarder la section qui parle des requêtes vers la base de données pour plus d'information

Cacher vos fichiers
=================================================

Une autre bonne pratique est ne laisser que votre *index.php*
et vos fichiers publiques (Par exemple .js, css et fichier d'images) à la racine de votre serveur (plus généralement nommée "htdocs/"). Ce sont les seuls fichiers que vous voulez laisser accessible de par le web.

Autoriser vos visiteurs a voir le reste pourrait potentiellement leur permettre d’accéder a des données sensible, des scripts d’exécution..

Si vous n'êtes pas autorisés à faire ça, vous pouvez essayer d'utiliser des fichiers .htaccess pour empêcher l'accès à ces ressources

CodeIgniter à un fichier index.html dans chacun de ses dossiers pour cacher certaines données, mais garder en tête que ce n'est pas suffisant pour se protéger d'attaque sérieuse.

