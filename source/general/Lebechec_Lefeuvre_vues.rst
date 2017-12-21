####
Vues
####
Une vue est simplement une page web, ou un fragment de page, comme l'en-tête, le pied de page,
une barre latérale, etc. En effet, les vues peuvent être facilement intégrées dans d'autres vues
(à l'intérieur d'autres vues, etc., etc.) Si vous avez besoin de ce type de hiérarchie.

On n'appelle jamais directement une vue, elles doivent être charger par un
:doc:`controleur <controllers>`. Il faut se rappeler que dans un Framework MVC (Modèle-Vues-Controleur), un 
controleur agit comme comme un agent de circulation, il est responsable pour récuperer les vues.
 Si vous n'avez pas encore lu la page
:doc:`Controleurs <controllers>` vous devriez le faire dans un premier temps.

En utilisant le controleur que vous venez de créer
:doc:`controleur <controllers>`, nous allons ajouter une vue à ce dernier.

Création d'une vue
==================

Créer un fichier vueBlog.php avec votre éditeur de texte, et y mettre le code
suivant::

	<html>
	<head>
		<title>Mon Blog</title>
	</head>
	<body>
		<h1>Bienvenue sur mon Blog!</h1>
	</body>
	</html>
	
Sauvegarder le fichier dans le dossier *application/views/* .

Chargement d'une vue
====================

Pour charger une vue vous devrez utiliser la méthode::

	$this->load->view('nom');

Ou nom est le nom de votre vue.

.. note:: L'extension .php n'a pas besoin d'être spécifiée sauf
si vous voulez faire autre chause q'un .php.

Maintenant, Ouvrir le controleur Blog.php que vous avez crée précedement, et
remplacer l'echo par la méthode de chargement de la vue::

	<?php
	class Blog extends CI_Controller {

		public function index()
		{
			$this->load->view('vueBlog');
		}
	}

Si vous visitez le site en utilisant l'url que vous avez crée précedement
vous devriez voir votre nouvelle vue.
L'url est similaire à cela::

	exemple.com/index.php/blog/

Charger plusieurs vues
======================

CodeIgniter va gérer intelligemment plusieurs appels
``$this->load->view()`` depuis un controleur. Si il y a plus d'un appel
ils seront gérés ensemble. Par exemple, Vous voudrez peut-être
une vue en-tête, une vue menu, vue contenu, et une vue pied de page. Ca
devrait resembler à cela::

	<?php

	class Page extends CI_Controller {

		public function index()
		{
			$data['titre_page'] = 'Votre titre';
			$this->load->view('en-tête');
			$this->load->view('menu');
			$this->load->view('contenu', $data);
			$this->load->view('pied-de-page');
		}

	}

Dans l'exemple ci-dessus, On utilise "Des données ajoutées dynamiquement", ce que vous
verez plus bas.

Stocker les vues dans des sous-dossiers
=======================================

Vos fichier de vue peuvent aussi être stocker à l'intérieur de sous-dossiers
si vous préferez ce type d'organisation.
En faisant cela vous aurez besoin d'inclure le nom du répertoire appelant les vues.
Exemple::

	$this->load->view('nom-du-repertoire/nom-du-fichier');

Ajout de données dynamique dans la vue
======================================

Les données sont transmises du controleur vers la vue par le biai d'un tableau
**array** ou d'un objet **object** dans le deuxième paramètre du chargement de la vue l.
Voici un exemple avec l'utilisation d'un tableau::

	$data = array(
		'titre' => 'Mon Titre',
		'en-tête' => 'Mon En-tête',
		'message' => 'Mon Message'
	);

	$this->load->view('vueBlog', $data);

Et voici un exemple avec un objet::

	$data = new Someclass();
	$this->load->view('vueBlog', $data);

.. note:: Si vous utilisez un objet, la variable va être changée
 en tableau.

On va essayer avec le controleur. Ouvrez le et ajoutez ce code::

	<?php
	class Blog extends CI_Controller {

		public function index()
		{
			$data['titre'] = "Mon vrai titre";
			$data['en-tête'] = "Ma vrai en-tête";

			$this->load->view('vueBlog', $data);
		}
	}

Maintenant ouvrez votre vue et changer le texte en variables qui correspond
au clés de votre tableau data::

	<html>
	<head>
		<title><?php echo $titre;?></title>
	</head>
	<body>
		<h1><?php echo $en-tête;?></h1>
	</body>
	</html>

Then load the page at the URL you've been using and you should see the
variables replaced.

Creating Loops
==============

The data array you pass to your view files is not limited to simple
variables. You can pass multi dimensional arrays, which can be looped to
generate multiple rows. For example, if you pull data from your database
it will typically be in the form of a multi-dimensional array.

Here's a simple example. Add this to your controller::

	<?php
	class Blog extends CI_Controller {

		public function index()
		{
			$data['todo_list'] = array('Clean House', 'Call Mom', 'Run Errands');

			$data['title'] = "My Real Title";
			$data['heading'] = "My Real Heading";

			$this->load->view('blogview', $data);
		}
	}

Now open your view file and create a loop::

	<html>
	<head>
		<title><?php echo $title;?></title>
	</head>
	<body>
		<h1><?php echo $heading;?></h1>
	
		<h3>My Todo List</h3>

		<ul>
		<?php foreach ($todo_list as $item):?>
	
			<li><?php echo $item;?></li>
	
		<?php endforeach;?>
		</ul>

	</body>
	</html>

.. note:: You'll notice that in the example above we are using PHP's
	alternative syntax. If you are not familiar with it you can read about
	it :doc:`here <alternative_php>`.

Returning views as data
=======================

There is a third **optional** parameter lets you change the behavior of
the method so that it returns data as a string rather than sending it
to your browser. This can be useful if you want to process the data in
some way. If you set the parameter to TRUE (boolean) it will return
data. The default behavior is false, which sends it to your browser.
Remember to assign it to a variable if you want the data returned::

	$string = $this->load->view('myfile', '', TRUE);