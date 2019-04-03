##############################
Handling Multiple Environments
##############################

Developers often desire different system behavior depending on whether
an application is running in a development or production environment.
For example, verbose error output is something that would be useful
while developing an application, but it may also pose a security issue
when "live".

L'environnement constant
========================

Par défault , CodeIgniter vient  avec la constante d'environnement à utiliser
avec la valeur fournie dans ``$_SERVER['CI_ENV']``, otherwise defaults to
'development'. Dans le haut de index.php, vous pouvez voir::

	define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development');

Cette variable peut être mise dans .htaccess file ou Apache 
avec la configuration que vous utilisez`SetEnv <https://httpd.apache.org/docs/2.2/mod/mod_env.html#setenv>`_. 
 
Des méthodes alternative existe pour nginx ou autre serveur ou bien vous pouvez supprimez ou tu peux
supprimer entièrement cette logique et définir la constante en fonction de l'adresse IP du serveur.
En plus d'affecter les comportements de base du framework ( consulter la section suivante), vous pouvez utiliser cette constante dans votre développement pour différencier
entre l'environnement que vous utilisez.

Effects On Default Framework Behavior
=====================================

There are some places in the CodeIgniter system where the ENVIRONMENT
constant is used. This section describes how default framework behavior
is affected.

Rapport d'erreur
---------------
Définir l'environnement constant à une valeur de "développement" va faire que toutes les erreurs PHP vont se rendre sur le navigateur lors du lancement.
À contrario, définir la "production" comme constante va désactiver toutes les sorties d'erreur. Désactiver les rapports d'erreur dans la production est une :doc:`bonne pratique de sécurité <security>` .

Si vous réglez la constante ENVIRONNEMENT sur la valeur de 'développement',
toutes les erreurs PHP à restituer au navigateur quand elles se produisent.
Inversement, le réglage de la constante sur «production» désactivera toutes les erreurs.
sortie. Désactiver le signalement des erreurs en production est un :doc:`bonne sécurité pour s'entraîner <security>`.

Configuration Files
=======
Fichiers de configuration

-------------------
Optionnellement, vous pouvez avoir le chargement de l'environnement spécifique des fichiers de configuration de CodeIgniter. Cela peut-être utile pour gérer des choses comme les Clés d'API différentes dans plusieurs environnements.
Ceci est décrit avec plus de détails dans la section de documentation :doc:`Configuration des classes <../libraries/config>`.