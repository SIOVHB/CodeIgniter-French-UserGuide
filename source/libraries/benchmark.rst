###################
Classe Benchmarking
###################

CodeIgniter dispose d'une classe dédiée au Benchmark qui est toujours active,
qui permet de calculer la différence de temps entre deux points marqués.

.. note:: Cette classe est initialisée automatiquement avec le système, il
	est donc inutile de le faire manuellement.

De plus, ce benchmark est toujours démarré au moment où le framework est
invoqué, et terminé quand la classe de sortie juste avant d'envoyer la
vue finale au navigateur, ce qui permet d'afficher un timing très précis
tout au long de l'affichage de l'éxecution du système.

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

****************************
Utiliser la classe Benchmark
****************************

La classe Benchmark peut être utilisée dans vos
:doc:`controleurs </general/controllers>`,
:doc:`vues </general/views>`, ou vos :doc:`modèles </general/models>`.
L'utilisation est la suivante:

#. Marquez un point de départ
#. Marquez un point de fin
#. Lancez la fonction de "temps écoulé" pour voir les résultats

Voici un exemple réel::

	$this->benchmark->mark('code_start');

	// Du code s'execute ici

	$this->benchmark->mark('code_end');

	echo $this->benchmark->elapsed_time('code_start', 'code_end');

.. note:: Les mots "code_start" et "code_end" sont arbitraires. Ce sont simplement des termes
	utilisés pour définir les deux marqueurs. Vous pouvez utiliser les mots que vous
	souhaitez, et pouvez définir plusieurs groupes de marqueurs. Voici quelques exemples::

		$this->benchmark->mark('dog');

		// Du code s'execute ici

		$this->benchmark->mark('cat');

		// Encore du code

		$this->benchmark->mark('bird');

		echo $this->benchmark->elapsed_time('dog', 'cat');
		echo $this->benchmark->elapsed_time('cat', 'bird');
		echo $this->benchmark->elapsed_time('dog', 'bird');


Profiler vos points de Benchmark
================================

Si vous voulez que vos données liées au Benchmark apparaissent dans le
:doc:`Profiler </general/profiling>` tout vos points marqués doivent être
parametrés en paire, et chaque marqueurs doivent finir avec _start et
_end. Autrement, chaques paires doivent être nommées de façon identique. Exemple::

	$this->benchmark->mark('my_mark_start');

	// Du code s'execute ici...

	$this->benchmark->mark('my_mark_end');

	$this->benchmark->mark('another_mark_start');

	// Encore plus de code s'execute ici...

	$this->benchmark->mark('another_mark_end');

Veuillez consulter la :doc:`page Profiler </general/profiling>` pour plus
plus d'informations.

Afficher le temps d'execution
===============================

Si vous voulez afficher le temps total écoulé entre le moment où
CodeIgniter démarre jusqu'au dernier affichage envoyé au navigateur,
placez ceci dans un de vos modèles::

	<?php echo $this->benchmark->elapsed_time();?>

Vous pouvez vous appercevoir qu'il s'agit de la même fonction utilisée dans
les exemples ci-dessus pour calculer le temps entre deux points,
sauf que vous n'utilisez **aucun** paramètre. Quand les paramètres sont absents,
CodeIgniter n'arrête le benchmark juste avant que le dernier affichage est envoyé
au navigateur. L'endroit où vous utilisez la fonction call ne change rien, le timer
continuera à s'executer jusqu'à la fin.

Une autre manière d'afficher le temps écoulé dans vos fichier de vues est
d'utiliser cette pseudo-variable, si vous ne voulez pas utiliser le PHP pur::

	{elapsed_time}

.. note:: Si vous voulez utiliser le benchmark sur toutes vos fonctions dans votre contrôleur,
	vous devez définir vous-même vos points de début/fin.

Afficher la consommation de mémoire
===================================

Si votre installation de php est configurée avec --enable-memory-limit, vous pouvez 
afficher la quantité de mémoire consommée par l'ensemble du système en 
utilisant le code suivant dans l'une de vos vue::

	<?php echo $this->benchmark->memory_usage();?>

.. note:: Cette fonction ne peut être utilisé dans vos vues. La consommation
	reflétera la mémoire totale utilisée par l'ensemble de l'application.

Une méthode alternative pour afficher la mémoire utilisé dans votre vue 
est d'utiliser cette pseudo-variable, si vous préféré ne pas utiliser le PHP pure::

	{memory_usage}


*******************
Référence de classe
*******************

.. php:class:: CI_Benchmark

	.. php:method:: mark($name)

		:param	string	$name: Le nom que vous voulez assigner au marqueur
		:rtype:	void

		Définit un marqueur de Benchmark.

	.. php:method:: elapsed_time([$point1 = ''[, $point2 = ''[, $decimals = 4]]])

		:param	string	$point1: un point particulier
		:param	string	$point2: un autre point particulier
		:param	int	$decimals: nombre de places décimales pour préciser
		:returns:	Temps écoulé
		:rtype:	string

		Calcule et retourne la différence de temps entre deux points marqués

		Si le premier paramètre est vide, cette fonction retourne à la place
		la pseudo-variable ``{elapsed_time}``. Cela permet au temps
		d'execution total de s'afficher dans une template. La classe output
		remplacera la vraie valeur par cette variable.


	.. php:method:: memory_usage()

		:returns:	Informations sur l'usage mémoire
		:rtype:	string

		Affiche simplement le marqueur ``{memory_usage}``.

		Il peut donc être placé n'importe où dans une template sans que la mémoire
		soit calculée avant la fin. La :doc:`classe Output <output>` remplacera
		la vraie valeur par cette variable.