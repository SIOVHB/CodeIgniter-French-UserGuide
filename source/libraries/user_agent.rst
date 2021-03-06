####################
LA classe User Agent 
####################

La classe User Agent fournit des fonctions qui permettent d'identifier les informations sur le navigateur,
appareil mobile ou robot qui visitent votre site. En outre, vous pouvez obtenir des informations r�f�r�s comme la langue et les informations des jeux de caract�res.
=======
#####################
La classe User Agent
#####################
La classe User Agent fournit des fonctions qui vous aideront à identifier des informations à propos
des navigateurs web, appareils mobiles ou les robots qui visitent votre site.
De plus, vous pouvez obtenir des informations telles que la langue et le jeu de caractères supporté.


.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>


***********************************
Utilisation de la classe User Agent
***********************************

Initialisation de la classe
===========================

Comme la plupart des autres classes de CodeIgniter, la classe User Agent est initialis�e dans votre contr�leur en utilisant la fonction $ this-> load-> biblioth�que:
=======
******************************
Utiliser la classe User Agent
******************************

Initialiser la classe
======================
Tout comme la plupart des classes dans CodeIgniter, la classe User Agent est initialisée dans votre contrôleur comme ceci : $this->load->library function

$this->load->library('user_agent');

Une fois charg�, l'objet sera disponible en utilisant: ``$this->agent``

D�finitions User Agent 
======================

Le nom des d�finitions de User Agent se trouvent dans un fichier de configuration situ� dans : application / config / user_agents.php. Vous pouvez ajouter des articles aux diff�rents tableaux de l'agent utilisateur si n�cessaire.

Exemple
=======

Lorsque la classe de l'agent utilisateur est initialis�e, il va tenter de d�terminer si l'agent utilisateur qui navigue votre site est sur un navigateur Web, un appareil mobile, ou un robot. Il sera �galement recueillir les informations de la plate-forme si elle est disponible.
=======
Une fois chargé, l'objet sera disponible en utilisant : ''$this->agent''

Définition de la classe User Agent
==================================

La classe user agent est définie dans le fichier de configuration situé sous:
application/config/user_agent.php. Vous pouvez ajouter des éléments aux tableaux de la classe
si c'est nécessaire

Exemples
=========

Lorsque la classe user agent est initialisée, elle va essayer de déterminer
si l'agent qui navigue dans votre site web est un navigateur web, un appareil mobile
ou un robot. Elle va également réunir des informations sur la plateforme si l'option est disponible


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
R�f�rence de la classe
**********************
=======
********************
Référence de classe
********************


.. php:class:: CI_User_agent

	.. php:method:: is_browser([$key = NULL])

		:param	string	$key: Optional browser name
		:returns:		
TRUE si l'agent utilisateur est un navigateur, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (bool�en) si l'agent utilisateur est un navigateur web connu.
=======
		:param	string	$key: Nom du navigateur (facultatif)
		:returns:	TRUE si l'agent est un navigateur (spécifique), FALSE si non
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

		.. note:: La cha�ne "Safari" dans cet exemple est une cl� de tableau dans la liste des d�finitions de navigateur. Vous pouvez trouver cette liste dans l' application / config / user_agents.php si vous souhaitez ajouter de nouveaux navigateurs ou modifier les chaines de caract�res.

	.. php:method:: is_mobile([$key = NULL])

		:param	string	$key:En option Nom du dispositif mobile
		:returns:		
TRUE si l'agent utilisateur est un p�riph�rique mobile, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (bool�en) si l'agent utilisateur est un appareil mobile connu.
=======
		.. note:: La chaîne de caractère "Safari" dans cet exemple est une clé du tableau listant tous les navigateurs.
			Vous pouvez trouver cette liste dans  **application/config/user_agents.php** si vous voulez ajouter des navigateurs ou changer certaines chaînes de caractères.
			

	.. php:method:: is_mobile([$key = NULL])

		:param	string	$key: nom de l'appareil mobile (facultatif)
		:returns:	TRUE si l'agent est un appareil mobile(spécifique), FALSE si non
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

		Retourne TRUE / FALSE (bool�en) si l'agent utilisateur est un robot connu.

		.. note:: La biblioth�que de l' agent utilisateur ne contient que des d�finitions de robots les plus courants. Il est pas une liste compl�te des bots. Il y a des centaines d'entre eux alors la recherche de chacun ne serait pas tr�s efficace. Si vous trouvez que certains robots qui visitent fr�quemment votre site sont absents de la liste , vous pouvez les ajouter � votre application / config / user_agents.php fichier.

	.. php:method:: is_referral()

		:returns:	TRUE si l'agent utilisateur est une r�f�rence, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (bool�en) si l'agent utilisateur a �t� renvoy� d'un autre site.

	.. php:method:: browser()

		:returns:	Navigateur d�tect� ou une cha�ne vide
		:rtype:	cha�ne

		Retourne une cha�ne contenant le nom du navigateur Web affichage de votre site.

	.. php:method:: version()

		:returns:	version du navigateur d�tect� ou une cha�ne vide
		:rtype:	cha�ne

		Retourne une cha�ne contenant le num�ro de version du navigateur Web affichage de votre site.

	.. php:method:: mobile()

		:returns:	la marque de l'appareil mobile d�tect� ou une cha�ne vide
		:rtype:	cha�ne

		Retourne une cha�ne contenant le nom de l'appareil mobile l'affichage de votre site.

	.. php:method:: robot()

		:returns:	nom de robot d�tect� ou une cha�ne vide
		:rtype:	cha�ne

		Retourne une cha�ne contenant le nom du robot affichage de votre site.

	.. php:method:: platform()

		:returns:	syst�me d'exploitation d�tect� ou une cha�ne vide
		:rtype:	chaine

		Retourne une cha�ne contenant la plate-forme de visualisation de votre site (Linux, Windows, OS X, etc.).

	.. php:method:: referrer()

		:returns:	referrer d�tect� ou une chaine vide
		:rtype:	string

		Le referrer, si l'agent utilisateur � �t� renvoy� vers un autre site. typiquement vous allez tester ceci comme suit.
=======
		:param	string	$key: le nom du robot (facultatif)
		:returns:	TRUE si l'agent est un robot (spécifique), FALSE si non
		:rtype:	bool

		Returns TRUE/FALSE (boolean)si l'agent est un robot connu.

		.. note:: La librairie de la classe user agent ne contient que les robots les plus connu. C'est une liste non    exhaustive. Il en existe des centaines donc les chercher un par un ne serait pas très efficace. Si vous trouvez des robots qui visite fréquament votre site web et qui ne sont pas référencé dans la liste vous pouvez les ajouter dans le fichier :
**application/config/user_agents.php**.
			

	.. php:method:: is_referral()

		:returns:	TRUE si l'agent utilisateur a été renvoyé d'un autre site, FALSE sinon
		:rtype:	bool

		

      Retourne TRUE / FALSE ( booléen ) si l'agent utilisateur a été renvoyé d'un autre site 

	.. php:method:: browser()

		:returns:	Le navigateur détecté ou une chaine vide 
		:rtype:	string

		Retourne une chaîne contenant le nom du navigateur Web avec lequel vous afficher le site.

	.. php:method:: version()

		:returns:	la version du navigateur détecté ou une chaine vide
		:rtype:	string

		Retourne une chaîne contenant la version du navigateur utiliser pour regarder le site.

	.. php:method:: mobile()

		:returns:      La marque de l'appareil mobile ou une chaine vide
		:rtype:	string

		Retourne une chaîne contenant le nom du dispositif mobile pour l'affichage de votre site.

	.. php:method:: robot()

		:returns:	Le nom du robot détecté ou une chaine vide
		:rtype:	string

		Retourne une chaîne contenant le nom du robot affichage de votre site.

	.. php:method:: platform()

		:returns:	L'OS détecté ou une chaine vide 
		:rtype:	string

		Retourne une chaîne contenant la plate-forme de visualisation de votre site (Linux, Windows, OS X, etc.).

	.. php:method:: referrer()

		:returns:	La référence détecté ou une chaine vide 
		:rtype:	string

		La référence si l'agent à été référé  à partir d'un autre site web. En règle général vous allez le tester comme ceci::


			if ($this->agent->is_referral())
			{
				echo $this->agent->referrer();
			}

	.. php:method:: agent_string()


		:returns:	La cha�ne compl�te de l'agent utilisateur ou une cha�ne vide
		:rtype:	Chaine

		Retourne une cha�ne contenant la cha�ne de l'agent utilisateur complet. Typiquement ce sera quelque chose comme �a:
=======
		:returns:	 Le nom complet de l'agent ou une chaine vide
		:rtype:	string

		Retourne une chaîne contenant la chaîne de l'agent utilisateur complet . En général, il sera quelque chose comme ceci::


			Mozilla/5.0 (Macintosh; U; Intel Mac OS X; en-US; rv:1.8.0.4) Gecko/20060613 Camino/1.0.2

	.. php:method:: accept_lang([$lang = 'en'])

		:param	string	$lang: Language key

		:returns:	TRUE Si la langue fourni est accept�e, FALSE sinon
		:rtype:	bool

		Permet de d�terminer si l'agent utilisateur accepte une langue particuli�re. Exemple:

			if ($this->agent->accept_lang('en'))
			{
				echo 'Vous acceptez anglais!';
			}

		.. note:: Cette m�thode est g�n�ralement tr�s fiable car certains navigateurs ne fournissent pas d'informations sur la langue, et m�me parmi ceux qui le font, il est pas toujours exacte.
=======
		:returns:	TRUE si la langue fournie est acceptée, FALSE si non
		:rtype:	bool

		Vous permet de déterminer si l'agent utilisateur accepte une langue particulière. Example::

			if ($this->agent->accept_lang('en'))
			{
				echo 'Vous pouvez utiliser l'anglais!';
			}

		.. note:: Cette méthode est généralement pas très fiable car certains navigateurs ne fournissent pas d'information de langue ,
et même parmi ceux qui le font , il n'est pas toujours exacte .


	.. php:method:: langages()


		:returns:	Un tableau avec la liste des languages accept�es
		:rtype:	Tableau

		Retourne un tableau de langues support� par les agent utilisateur.

	.. php:method:: accept_charset([$charset = 'utf-8'])

		:param	string	$charset: Jeu de charact�res
		:returns:	TRUE si le jeu de caract�res est accept�e, FALSE sinon
		:rtype:	bool

		Permet de d�terminer si l'agent utilisateur accepte un jeu de caract�res particulier. Exemple::

			if ($this->agent->accept_charset('utf-8'))
			{
				echo 'Votre navigateur support l'UTF-8!';
			}

		.. note:: Cette m�thode est g�n�ralement tr�s fiable car certains navigateurs ne fournissent pas d'informations de jeu de caract�res, et m�me parmi ceux qui le font, il est pas toujours exacte.

	.. php:method:: charsets()

		:returns:	Une liste de tableau de jeux de caract�res accept�s
		:rtype:	Tableau

		Retourne un tableau de jeux de caract�res accept�s par l'agent utilisateur.
=======
		:returns:	Un tableau de la liste des langues acceptées
		:rtype:	array

		Retourne un tableau de langues prises en charge par l'agent utilisateur .

	.. php:method:: accept_charset([$charset = 'utf-8'])

		:param	string	$charset: Jeu de caractère 
		:returns:	TRUE si le jeu de caractère est accepté, FALSE si non 
		:rtype:	bool

		Vous permet de déterminer si l'agent utilisateur accepte un jeu de caractères particulier. Exemple::

			if ($this->agent->accept_charset('utf-8'))
			{
				echo 'Votre navigateur supporte  UTF-8!';
			}

		.. note:: Cette méthode n'est généralement pas très fiable car certains navigateurs ne fournissent pas d'informations de jeu de caractères ,
et même parmi ceux qui le font , il n'est pas toujours exacte .

	.. php:method:: charsets()

		:returns:	Un tableau contenant la liste des jeux de caractères acceptés
		:rtype:	array

		Retourne un tableau de jeux de caractères acceptés par l'agent utilisateur .


	.. php:method:: parse($string)

		:param	string	$string: Une chaine personalis� user-agent string
		:rtype:	Vide


		Parses une cha�ne user-agent personnalis�, diff�rent de celui rapport� par le visiteur actuel
=======
		Parses est une chaîne user-agent personnalisé , différent de celui rapporté par le visiteur actuel.

