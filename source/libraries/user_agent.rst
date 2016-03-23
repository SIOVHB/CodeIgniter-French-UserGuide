####################
LA classe User Agent 
####################

La classe User Agent fournit des fonctions qui permettent d'identifier les informations sur le navigateur,
appareil mobile ou robot qui visitent votre site. En outre, vous pouvez obtenir des informations référés comme la langue et les informations des jeux de caractères.

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

***********************************
Utilisation de la classe User Agent
***********************************

Initialisation de la classe
===========================

Comme la plupart des autres classes de CodeIgniter, la classe User Agent est initialisée dans votre contrôleur en utilisant la fonction $ this-> load-> bibliothèque:

	$this->load->library('user_agent');

Une fois chargé, l'objet sera disponible en utilisant: ``$this->agent``

Définitions User Agent 
======================

Le nom des définitions de User Agent se trouvent dans un fichier de configuration situé dans : application / config / user_agents.php. Vous pouvez ajouter des articles aux différents tableaux de l'agent utilisateur si nécessaire.

Exemple
=======

Lorsque la classe de l'agent utilisateur est initialisée, il va tenter de déterminer si l'agent utilisateur qui navigue votre site est sur un navigateur Web, un appareil mobile, ou un robot. Il sera également recueillir les informations de la plate-forme si elle est disponible.

::

	$this->load->library('user_agent');

	if ($this->agent->is_browser())
	{
		$agent = $this->agent->browser().' '.$this->agent->version();
	}
	elseif ($this->agent->is_robot())
	{
		$agent = $this->agent->robot();
	}
	elseif ($this->agent->is_mobile())
	{
		$agent = $this->agent->mobile();
	}
	else
	{
		$agent = 'Unidentified User Agent';
	}

	echo $agent;

	echo $this->agent->platform(); // Platform info (Windows, Linux, Mac, etc.)

**********************
Référence de la classe
**********************

.. php:class:: CI_User_agent

	.. php:method:: is_browser([$key = NULL])

		:param	string	$key: Optional browser name
		:returns:		
TRUE si l'agent utilisateur est un navigateur, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (booléen) si l'agent utilisateur est un navigateur web connu.
		::

			if ($this->agent->is_browser('Safari'))
			{
				echo 'Vous utilisez Safari.';
			}
			elseif ($this->agent->is_browser())
			{
				echo 'Vous utilisez un navigateur.';
			}

		.. note:: La chaîne "Safari" dans cet exemple est une clé de tableau dans la liste des définitions de navigateur. Vous pouvez trouver cette liste dans l' application / config / user_agents.php si vous souhaitez ajouter de nouveaux navigateurs ou modifier les chaines de caractères.

	.. php:method:: is_mobile([$key = NULL])

		:param	string	$key:En option Nom du dispositif mobile
		:returns:		
TRUE si l'agent utilisateur est un périphérique mobile, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (booléen) si l'agent utilisateur est un appareil mobile connu.
		::

			if ($this->agent->is_mobile('iphone'))
			{
				$this->load->view('iphone/home');
			}
			elseif ($this->agent->is_mobile())
			{
				$this->load->view('mobile/home');
			}
			else
			{
				$this->load->view('web/home');
			}

	.. php:method:: is_robot([$key = NULL])

		:param	string	$key: En option nom de robot
		:returns:		
TRUE si l'agent utilisateur est un robot, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (booléen) si l'agent utilisateur est un robot connu.

		.. note:: La bibliothèque de l' agent utilisateur ne contient que des définitions de robots les plus courants. Il est pas une liste complète des bots. Il y a des centaines d'entre eux alors la recherche de chacun ne serait pas très efficace. Si vous trouvez que certains robots qui visitent fréquemment votre site sont absents de la liste , vous pouvez les ajouter à votre application / config / user_agents.php fichier.

	.. php:method:: is_referral()

		:returns:	TRUE si l'agent utilisateur est une référence, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (booléen) si l'agent utilisateur a été renvoyé d'un autre site.

	.. php:method:: browser()

		:returns:	Navigateur détecté ou une chaîne vide
		:rtype:	chaîne

		Retourne une chaîne contenant le nom du navigateur Web affichage de votre site.

	.. php:method:: version()

		:returns:	version du navigateur détecté ou une chaîne vide
		:rtype:	chaîne

		Retourne une chaîne contenant le numéro de version du navigateur Web affichage de votre site.

	.. php:method:: mobile()

		:returns:	la marque de l'appareil mobile détecté ou une chaîne vide
		:rtype:	chaîne

		Retourne une chaîne contenant le nom de l'appareil mobile l'affichage de votre site.

	.. php:method:: robot()

		:returns:	nom de robot détecté ou une chaîne vide
		:rtype:	chaîne

		Retourne une chaîne contenant le nom du robot affichage de votre site.

	.. php:method:: platform()

		:returns:	système d'exploitation détecté ou une chaîne vide
		:rtype:	chaine

		Retourne une chaîne contenant la plate-forme de visualisation de votre site (Linux, Windows, OS X, etc.).

	.. php:method:: referrer()

		:returns:	referrer détecté ou une chaine vide
		:rtype:	string

		Le referrer, si l'agent utilisateur à été renvoyé vers un autre site. typiquement vous allez tester ceci comme suit.

			if ($this->agent->is_referral())
			{
				echo $this->agent->referrer();
			}

	.. php:method:: agent_string()

		:returns:	La chaîne complète de l'agent utilisateur ou une chaîne vide
		:rtype:	Chaine

		Retourne une chaîne contenant la chaîne de l'agent utilisateur complet. Typiquement ce sera quelque chose comme ça:

			Mozilla/5.0 (Macintosh; U; Intel Mac OS X; en-US; rv:1.8.0.4) Gecko/20060613 Camino/1.0.2

	.. php:method:: accept_lang([$lang = 'en'])

		:param	string	$lang: Language key
		:returns:	TRUE Si la langue fourni est acceptée, FALSE sinon
		:rtype:	bool

		Permet de déterminer si l'agent utilisateur accepte une langue particulière. Exemple:

			if ($this->agent->accept_lang('en'))
			{
				echo 'Vous acceptez anglais!';
			}

		.. note:: Cette méthode est généralement très fiable car certains navigateurs ne fournissent pas d'informations sur la langue, et même parmi ceux qui le font, il est pas toujours exacte.

	.. php:method:: langages()

		:returns:	Un tableau avec la liste des languages acceptées
		:rtype:	Tableau

		Retourne un tableau de langues supporté par les agent utilisateur.

	.. php:method:: accept_charset([$charset = 'utf-8'])

		:param	string	$charset: Jeu de charactères
		:returns:	TRUE si le jeu de caractères est acceptée, FALSE sinon
		:rtype:	bool

		Permet de déterminer si l'agent utilisateur accepte un jeu de caractères particulier. Exemple::

			if ($this->agent->accept_charset('utf-8'))
			{
				echo 'Votre navigateur support l'UTF-8!';
			}

		.. note:: Cette méthode est généralement très fiable car certains navigateurs ne fournissent pas d'informations de jeu de caractères, et même parmi ceux qui le font, il est pas toujours exacte.

	.. php:method:: charsets()

		:returns:	Une liste de tableau de jeux de caractères acceptés
		:rtype:	Tableau

		Retourne un tableau de jeux de caractères acceptés par l'agent utilisateur.

	.. php:method:: parse($string)

		:param	string	$string: Une chaine personalisé user-agent string
		:rtype:	Vide

		Parses une chaîne user-agent personnalisé, différent de celui rapporté par le visiteur actuel