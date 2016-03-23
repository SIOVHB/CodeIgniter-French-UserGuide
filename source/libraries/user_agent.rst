####################
LA classe User Agent 
####################

La classe User Agent fournit des fonctions qui permettent d'identifier les informations sur le navigateur,
appareil mobile ou robot qui visitent votre site. En outre, vous pouvez obtenir des informations r�f�r�s comme la langue et les informations des jeux de caract�res.

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

	$this->load->library('user_agent');

Une fois charg�, l'objet sera disponible en utilisant: ``$this->agent``

D�finitions User Agent 
======================

Le nom des d�finitions de User Agent se trouvent dans un fichier de configuration situ� dans : application / config / user_agents.php. Vous pouvez ajouter des articles aux diff�rents tableaux de l'agent utilisateur si n�cessaire.

Exemple
=======

Lorsque la classe de l'agent utilisateur est initialis�e, il va tenter de d�terminer si l'agent utilisateur qui navigue votre site est sur un navigateur Web, un appareil mobile, ou un robot. Il sera �galement recueillir les informations de la plate-forme si elle est disponible.

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
R�f�rence de la classe
**********************

.. php:class:: CI_User_agent

	.. php:method:: is_browser([$key = NULL])

		:param	string	$key: Optional browser name
		:returns:		
TRUE si l'agent utilisateur est un navigateur, FALSE sinon
		:rtype:	bool

		Retourne TRUE / FALSE (bool�en) si l'agent utilisateur est un navigateur web connu.
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

			if ($this->agent->is_referral())
			{
				echo $this->agent->referrer();
			}

	.. php:method:: agent_string()

		:returns:	La cha�ne compl�te de l'agent utilisateur ou une cha�ne vide
		:rtype:	Chaine

		Retourne une cha�ne contenant la cha�ne de l'agent utilisateur complet. Typiquement ce sera quelque chose comme �a:

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

	.. php:method:: parse($string)

		:param	string	$string: Une chaine personalis� user-agent string
		:rtype:	Vide

		Parses une cha�ne user-agent personnalis�, diff�rent de celui rapport� par le visiteur actuel