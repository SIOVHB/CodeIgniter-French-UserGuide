######
Modèle
######


Les modèles disponibles sont **optionnel** pour ceux qui veulent utiliser une approche MVC.

.. contents:: Contenu de la page

Qu'est ce qu'un modèle?
================


Les modèles sont des classes PHP qui sont faites pour travailler avec les informations des bases de données. Par exemple, disons que vous utilisez CodeIgniter pour gérer un blog. Vous aurez un modèle de classe qui contient des fonctions pour insérer/extraire des données et les mettre à jour.
Voici un exemple de classe du modèle.

	class Blog_model extends CI_Model {

		public $title;
		public $content;
		public $date;

		public function __construct()
		{
			// Appelle le constructeur CI modèle.
			parent::__construct();
		}

		public function get_last_ten_entries()
		{
			$query = $this->db->get('entries', 10);
			return $query->result();
		}

		public function insert_entry()
		{
			$this->title	= $_POST['title']; // lire les note ci-dessous
			$this->content	= $_POST['content'];
			$this->date	= time();

			$this->db->insert('entries', $this);
		}

		public function update_entry()
		{
			$this->title	= $_POST['title'];
			$this->content	= $_POST['content'];
			$this->date	= time();

			$this->db->update('entries', $this, array('id' => $_POST['id']));
		}

	}

.. note:: La méthode au dessus de l’exemple utilise  les :doc:`Query Builder
	<../database/query_builder>` méthodes de base de données
.. note:: Pour simplifier dans cet exemple, nous utilisons ``$_POST``
	directement . C'est généralement une mauvaise manière d'utiliser une variable $_POST directement, la manière la plus idéale serais de cette façon :doc:`Input Library <../libraries/input>`
	``$this->input->post('title')``.

Anatomie du modèle
==================

Les classes d'un modèle sont stockéss dans le répertoire **application/models/**.
Elles peuvent être implanter dans ce sous répertoire si vous voulez se type d'organisation de code.

Le prototype basique pour une classe modèle est comme ça::

	class Model_name extends CI_Model {

		public function __construct()
		{
			parent::__construct();
		}

	}


Où **Model_name** est le nom de la classe. Les noms de classes **doivent** avoir la notation Camel.
Faire en sorte que la classe hérite la classe du modèle de base.

Le nom du fichier doit correspondre au nom de la classe. Voici un exemple::

	class User_model extends CI_Model {

		public function __construct()
		{
			parent::__construct();
		}

	}

Le fichier sera comme ça::

	application/models/User_model.php

Chargement d'un modèle.
===============


Votre modèle sera typiquement chargé et appelé depuis les méthodes du contrôleurs.
Pour charger un modèle vous allez utiliser cette méthode::
	$this->load->model('model_name');

Si votre modèle est situé dans un sous répertoire, incluez le chemin relatif du répertoire modèle. Par exemple, si vous avez un modèle situé à *application/models/blog/Queries.php* vous allez l’appeler avec la commande ci-dessous:: 

	$this->load->model('blog/queries');

Une fois chargé, vous allez accéder au méthode du modèle utilisant un objet avec le même nom de votre classe::

	$this->load->model('model_name');

	$this->model_name->method();

Si vous voulez assigner un modèle à un objet différent, on peut le spécifier via un second paramètre dans la méthode de chargement::

	$this->load->model('model_name', 'foobar');

	$this->foobar->method();


Voici un exemple d'un controleur qui charge un modèle, qui charge une vue::

	class Blog_controller extends CI_Controller {

		public function blog()
		{
			$this->load->model('blog');

			$data['query'] = $this->blog->get_last_ten_entries();

			$this->load->view('blog', $data);
		}
	}
	

Chargement automatique d'un modèle.
===================



Si vous pensez que vous aurez besoin d'un modèle particulier globalement tout au long de votre application, vous pouvez assignez à CodeIgniter d’auto-charger le modèle durant l'initialisation du système. Cela peut être fait en ouvrant le fichier autoload.php se situant dans le répertoire **appplication/config/autoload.php** et ajouter le modèle dans le tableau d'auto-chargement (autoload array).


Connexion à la base de données
===========================

Quand un modèle est chargé il ne se connecte pas automatiquement à votre base de donnée.
Voici les méthodes disponibles pour se connecter à votre base:


 - Vous pouvez connecter  la base en utilisant la méthode standard :doc:`décrit ici <../database/connecting>`,soit à partir de votre classe Controller ou de votre classe Model.

 - Vous pouvez assigner au modèle de charger la méthode d'auto-connexion en passant la valeur vrai (TRUE(boolean)) qui est une   valeur booléenne via le troisième paramètre, et les paramètres de connectivité,
comme défini dans votre fichier de configuration de base de données sera utilisé comme cela ::

	$this->load->model('model_name', '', TRUE);

- Vous pouvez manuellement configurer les paramètres de connexion de la base de données via le troisième paramètre::

	$config['hostname'] = 'localhost';
	$config['username'] = 'myusername';
	$config['password'] = 'mypassword';
	$config['database'] = 'mydatabase';
	$config['dbdriver'] = 'mysqli';
	$config['dbprefix'] = '';
	$config['pconnect'] = FALSE;
	$config['db_debug'] = TRUE;

	$this->load->model('model_name', '', $config);