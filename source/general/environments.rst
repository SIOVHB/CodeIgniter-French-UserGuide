########################################
Prendre en main plusieurs environnements
########################################


Les développeurs veulent souvent avoir différents comportements de systèmes selon
l'application en exécution dans un environnement de développement ou de production.
Par exemple, une sortie des erreurs détaillées serait utile pendant le développement
d'une application, mais cela peut poser un problème de sécurité lorsque celle ci est active.

The ENVIRONMENT Constant
========================

By default, CodeIgniter comes with the environment constant set to use
the value provided in ``$_SERVER['CI_ENV']``, otherwise defaults to
'development'. At the top of index.php, you will see::

	define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development');

This server variable can be set in your .htaccess file, or Apache 
config using `SetEnv <https://httpd.apache.org/docs/2.2/mod/mod_env.html#setenv>`_. 
Alternative methods are available for nginx and other servers, or you can 
remove this logic entirely and set the constant based on the server's IP address.

In addition to affecting some basic framework behavior (see the next
section), you may use this constant in your own development to
differentiate between which environment you are running in.

Les effets sur le comportement par défaut du framework
======================================================

Il y a des endroits dans le système de CodeIgniter où l'environnement constant est utilisé.
Cette section décrit comment le comportement par défaut du framework est affecté.

Rapport d'erreur
---------------
Définir l'environnement constant à une valeur de "développement" va faire que toutes les erreurs PHP vont se rendre sur le navigateur lors du lancement.
À contrario, définir la "production" comme constante va désactiver toutes les sorties d'erreur. Désactiver les rapports d'erreur dans la production est une :doc:`bonne pratique de sécurité <security>` .

Fichiers de configuration
-------------------
Optionnellement, vous pouvez avoir le chargement de l'environnement spécifique des fichiers de configuration de CodeIgniter. Cela peut-être utile pour gérer des choses comme les Clés d'API différentes dans plusieurs environnements.
Ceci est décrit avec plus de détails dans la section de documentation :doc:`Configuration des classes <../libraries/config>`.