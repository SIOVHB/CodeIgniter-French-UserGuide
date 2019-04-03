####################
LA classe User Agent 
####################

La classe User Agent fournit des fonctions qui permettent d'identifier les informations sur le navigateur,
appareil mobile ou robot qui visitent votre site. En outre, vous pouvez obtenir des informations référés comme la langue et les informations des jeux de caractères.
=======
#####################
La classe User Agent
#####################
La classe User Agent fournit des fonctions qui vous aideront Ã  identifier des informations Ã  propos
des navigateurs web, appareils mobiles ou les robots qui visitent votre site.
De plus, vous pouvez obtenir des informations telles que la langue et le jeu de caractÃ¨res supportÃ©.


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
=======
******************************
Utiliser la classe User Agent
******************************

Initialiser la classe
======================
Tout comme la plupart des classes dans CodeIgniter, la classe User Agent est initialisÃ©e dans votre contrÃ´leur comme ceci : $this->load->library function

$this->load->library('user_agent');

Une fois chargé, l'objet sera disponible en utilisant: ``$this->agent``

Définitions User Agent 
======================

Le nom des définitions de User Agent se trouvent dans un fichier de configuration situé dans : application / config / user_agents.php. Vous pouvez ajouter des articles aux différents tableaux de l'agent utilisateur si nécessaire.

Exemple
=======

Lorsque la classe de l'agent utilisateur est initialisée, il va tenter de déterminer si l'agent utilisateur qui navigue votre site est sur un navigateur Web, un appareil mobile, ou un robot. Il sera également recueillir les informations de la plate-forme si elle est disponible.
=======
Une fois chargÃ©, l'objet sera disponible en utilisant : ''$this->agent''

DÃ©finition de la classe User Agent
==================================

La classe user agent est dÃ©finie dans le fichier de configuration situÃ© sous:
application/config/user_agent.php. Vous pouvez ajouter des Ã©lÃ©ments aux tableaux de la classe
si c'est nÃ©cessaire

Exemples
=========

Lorsque la classe user agent est initialisÃ©e, elle va essayer de dÃ©terminer
si l'agent qui navigue dans votre site web est un navigateur web, un appareil mobile
ou un robot. Elle va Ã©galement rÃ©unir des informations sur la plateforme si l'option est disponible


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

	echo $this->agent->platform(); // information sur la plateforme (Windows, Linux, Mac, etc.)

**********************
Référence de la classe
**********************
=======
********************
RÃ©fÃ©rence de classe
********************


.. php:class:: CI_User_agent

	.. php:method:: is_browser([$key = NULL])

		:param	string	$key: Optional browser name
		:returns:		
TRUE si l'agent utilisateur est un navigateur, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (booléen) si l'agent utilisateur est un navigateur web connu.
=======
		:param	string	$key: Nom du navigateur (facultatif)
		:returns:	TRUE si l'agent est un navigateur (spÃ©cifique), FALSE si non
		:rtype:	bool

		Retourne TRUE/FALSE (boolean)si l'agent est un navigateur connu.

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
=======
		.. note:: La chaÃ®ne de caractÃ¨re "Safari" dans cet exemple est une clÃ© du tableau listant tous les navigateurs.
			Vous pouvez trouver cette liste dans  **application/config/user_agents.php** si vous voulez ajouter des navigateurs ou changer certaines chaÃ®nes de caractÃ¨res.
			

	.. php:method:: is_mobile([$key = NULL])

		:param	string	$key: nom de l'appareil mobile (facultatif)
		:returns:	TRUE si l'agent est un appareil mobile(spÃ©cifique), FALSE si non
		:rtype:	bool

		Returns TRUE/FALSE (boolean) si l'agent est un appareil mobile connu.

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
=======
		:param	string	$key: le nom du robot (facultatif)
		:returns:	TRUE si l'agent est un robot (spÃ©cifique), FALSE si non
		:rtype:	bool

		Returns TRUE/FALSE (boolean)si l'agent est un robot connu.

		.. note:: La librairie de la classe user agent ne contient que les robots les plus connu. C'est une liste non    exhaustive. Il en existe des centaines donc les chercher un par un ne serait pas trÃ¨s efficace. Si vous trouvez des robots qui visite frÃ©quament votre site web et qui ne sont pas rÃ©fÃ©rencÃ© dans la liste vous pouvez les ajouter dans le fichier :
**application/config/user_agents.php**.
			

	.. php:method:: is_referral()

		:returns:	TRUE si l'agent utilisateur a Ã©tÃ© renvoyÃ© d'un autre site, FALSE sinon
		:rtype:	bool

		

      Retourne TRUE / FALSE ( boolÃ©en ) si l'agent utilisateur a Ã©tÃ© renvoyÃ© d'un autre site 

	.. php:method:: browser()

		:returns:	Le navigateur dÃ©tectÃ© ou une chaine vide 
		:rtype:	string

		Retourne une chaÃ®ne contenant le nom du navigateur Web avec lequel vous afficher le site.

	.. php:method:: version()

		:returns:	la version du navigateur dÃ©tectÃ© ou une chaine vide
		:rtype:	string

		Retourne une chaÃ®ne contenant la version du navigateur utiliser pour regarder le site.

	.. php:method:: mobile()

		:returns:      La marque de l'appareil mobile ou une chaine vide
		:rtype:	string

		Retourne une chaÃ®ne contenant le nom du dispositif mobile pour l'affichage de votre site.

	.. php:method:: robot()

		:returns:	Le nom du robot dÃ©tectÃ© ou une chaine vide
		:rtype:	string

		Retourne une chaÃ®ne contenant le nom du robot affichage de votre site.

	.. php:method:: platform()

		:returns:	L'OS dÃ©tectÃ© ou une chaine vide 
		:rtype:	string

		Retourne une chaÃ®ne contenant la plate-forme de visualisation de votre site (Linux, Windows, OS X, etc.).

	.. php:method:: referrer()

		:returns:	La rÃ©fÃ©rence dÃ©tectÃ© ou une chaine vide 
		:rtype:	string

		La rÃ©fÃ©rence si l'agent Ã  Ã©tÃ© rÃ©fÃ©rÃ©  Ã  partir d'un autre site web. En rÃ¨gle gÃ©nÃ©ral vous allez le tester comme ceci::


			if ($this->agent->is_referral())
			{
				echo $this->agent->referrer();
			}

	.. php:method:: agent_string()


		:returns:	La chaîne complète de l'agent utilisateur ou une chaîne vide
		:rtype:	Chaine

		Retourne une chaîne contenant la chaîne de l'agent utilisateur complet. Typiquement ce sera quelque chose comme ça:
=======
		:returns:	 Le nom complet de l'agent ou une chaine vide
		:rtype:	string

		Retourne une chaÃ®ne contenant la chaÃ®ne de l'agent utilisateur complet . En gÃ©nÃ©ral, il sera quelque chose comme ceci::


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
=======
		:returns:	TRUE si la langue fournie est acceptÃ©e, FALSE si non
		:rtype:	bool

		Vous permet de dÃ©terminer si l'agent utilisateur accepte une langue particuliÃ¨re. Example::

			if ($this->agent->accept_lang('en'))
			{
				echo 'Vous pouvez utiliser l'anglais!';
			}

		.. note:: Cette mÃ©thode est gÃ©nÃ©ralement pas trÃ¨s fiable car certains navigateurs ne fournissent pas d'information de langue ,
et mÃªme parmi ceux qui le font , il n'est pas toujours exacte .


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
=======
		:returns:	Un tableau de la liste des langues acceptÃ©es
		:rtype:	array

		Retourne un tableau de langues prises en charge par l'agent utilisateur .

	.. php:method:: accept_charset([$charset = 'utf-8'])

		:param	string	$charset: Jeu de caractÃ¨re 
		:returns:	TRUE si le jeu de caractÃ¨re est acceptÃ©, FALSE si non 
		:rtype:	bool

		Vous permet de dÃ©terminer si l'agent utilisateur accepte un jeu de caractÃ¨res particulier. Exemple::

			if ($this->agent->accept_charset('utf-8'))
			{
				echo 'Votre navigateur supporte  UTF-8!';
			}

		.. note:: Cette mÃ©thode n'est gÃ©nÃ©ralement pas trÃ¨s fiable car certains navigateurs ne fournissent pas d'informations de jeu de caractÃ¨res ,
et mÃªme parmi ceux qui le font , il n'est pas toujours exacte .

	.. php:method:: charsets()

		:returns:	Un tableau contenant la liste des jeux de caractÃ¨res acceptÃ©s
		:rtype:	array

		Retourne un tableau de jeux de caractÃ¨res acceptÃ©s par l'agent utilisateur .


	.. php:method:: parse($string)

		:param	string	$string: Une chaine personalisé user-agent string
		:rtype:	Vide


		Parses une chaîne user-agent personnalisé, différent de celui rapporté par le visiteur actuel
=======
		Parses est une chaÃ®ne user-agent personnalisÃ© , diffÃ©rent de celui rapportÃ© par le visiteur actuel.

