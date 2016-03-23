################
Pagination Class
################

la classe pagination de CodeIgniers est très facile à utiliser, et est entièrement personnalisable,
autant de maniere dynamique que via des préférences enregistrés.

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

Si vous n'etes pas familier avec le terme "Pagination", il fait références aux liens permettant de 
naviger d'une page à l'autre tel que :

	« First  < 1 2 3 4 5 >  Last »

*******
Exemple
*******


C'est un petit exemple pour vous montrer comment ajouter la pagination dans
l'une de vos méthodes du :doc:`controller <../general/controllers>`
=======
Voici un exemple simple montrant comment créer une pagination dans l'un de vos :doc:`controller <../general/controllers>` de méthodes :

	$this->load->library('pagination');

	$config['base_url'] = 'http://example.com/index.php/test/page/';
	$config['total_rows'] = 200;
	$config['per_page'] = 20;

	$this->pagination->initialize($config);

	echo $this->pagination->create_links();

Notes
=====

le tableau "$config" contient vos variables de configuration. Elle sont
 transmisent vers la méthode ``$this->pagination->initialize()`` comme indiqué
 ci dessus. Bien qu'il y ait une vingtaine d'items configurable, vous n'avez qu'a 
 en représenter 3. Voici une description de ces trois items. 

-  **base_url** Ceci est l'url complète du controleur de la classe/fonction contenant votre
pagination. Dans l'exemple ci-dessus, il est diriger vers un contrôleur appelé "Test" et vers une 
fonction appelé "page". Gardez en tête que :
-Vous pouvez router votre url <../general/routing> si vous avez besoin d'une structure différente.
	
TOTAL_ROWS Ce nombre représente le nombre total de lignes dans le jeu de résultats que vous créez 
la pagination pour. Généralement , ce nombre sera le nombre total de lignes que votre requête de base
 de données retournée.
-  **per_page** Le nombre d'articles que vous souhaitez afficher par page. Dans l'exemple ci - dessus, 
vous montrerez 20 items par page.
The ``create_links()`` method returns an empty string when there is no
pagination to show.

Setting preferences in a config file
====================================

If you prefer not to set preferences using the above method, you can
instead put them into a config file. Simply create a new file called
pagination.php, add the ``$config`` array in that file. Then save the file
in *application/config/pagination.php* and it will be used automatically.
You will NOT need to use ``$this->pagination->initialize()`` if you save
your preferences in a config file.

**************************
Customizing the Pagination
**************************

The following is a list of all the preferences you can pass to the
initialization function to tailor the display.

**$config['uri_segment'] = 3;**

The pagination function automatically determines which segment of your
URI contains the page number. If you need something different you can
specify it.

**$config['num_links'] = 2;**

The number of "digit" links you would like before and after the selected
page number. For example, the number 2 will place two digits on either
side, as in the example links at the very top of this page.

**$config['use_page_numbers'] = TRUE;**

By default, the URI segment will use the starting index for the items
you are paginating. If you prefer to show the the actual page number,
set this to TRUE.

**$config['page_query_string'] = TRUE;**

By default, the pagination library assume you are using :doc:`URI
Segments <../general/urls>`, and constructs your links something
like::

	http://example.com/index.php/test/page/20

If you have ``$config['enable_query_strings']`` set to TRUE your links
will automatically be re-written using Query Strings. This option can
also be explictly set. Using ``$config['page_query_string']`` set to TRUE,
the pagination link will become::

	http://example.com/index.php?c=test&m=page&per_page=20

Note that "per_page" is the default query string passed, however can be
configured using ``$config['query_string_segment'] = 'your_string'``

**$config['reuse_query_string'] = FALSE;**

By default your Query String arguments (nothing to do with other
query string options) will be ignored. Setting this config to
TRUE will add existing query string arguments back into the
URL after the URI segment and before the suffix.::

	http://example.com/index.php/test/page/20?query=search%term

This helps you mix together normal :doc:`URI Segments <../general/urls>`
as well as query string arguments, which until 3.0 was not possible.

**$config['prefix'] = '';**

A custom prefix added to the path. The prefix value will be right before
the offset segment.

**$config['suffix'] = '';**

A custom suffix added to the path. The sufix value will be right after
the offset segment.

**$config['use_global_url_suffix'] = FALSE;**

When set to TRUE, it will **override** the ``$config['suffix']`` value and
instead set it to the one that you have in ``$config['url_suffix']`` in
your **application/config/config.php** file.

***********************
Adding Enclosing Markup
***********************

If you would like to surround the entire pagination with some markup you
can do it with these two preferences:

**$config['full_tag_open'] = '<p>';**

The opening tag placed on the left side of the entire result.

**$config['full_tag_close'] = '</p>';**

The closing tag placed on the right side of the entire result.

**************************
Customizing the First Link
**************************

**$config['first_link'] = 'First';**

The text you would like shown in the "first" link on the left. If you do
not want this link rendered, you can set its value to FALSE.

.. note:: This value can also be translated via a language file.

**$config['first_tag_open'] = '<div>';**

The opening tag for the "first" link.

**$config['first_tag_close'] = '</div>';**

The closing tag for the "first" link.

**$config['first_url'] = '';**

An alternative URL to use for the "first page" link.

*************************
Customizing the Last Link
*************************

**$config['last_link'] = 'Last';**

The text you would like shown in the "last" link on the right. If you do
not want this link rendered, you can set its value to FALSE.

.. note:: This value can also be translated via a language file.

**$config['last_tag_open'] = '<div>';**

The opening tag for the "last" link.

**$config['last_tag_close'] = '</div>';**

The closing tag for the "last" link.

***************************
Customizing the "Next" Link
***************************

**$config['next_link'] = '&gt;';**

The text you would like shown in the "next" page link. If you do not
want this link rendered, you can set its value to FALSE.

.. note:: This value can also be translated via a language file.

**$config['next_tag_open'] = '<div>';**

The opening tag for the "next" link.

**$config['next_tag_close'] = '</div>';**

The closing tag for the "next" link.

*******************************
Customizing the "Previous" Link
*******************************

**$config['prev_link'] = '&lt;';**

The text you would like shown in the "previous" page link. If you do not
want this link rendered, you can set its value to FALSE.

.. note:: This value can also be translated via a language file.

**$config['prev_tag_open'] = '<div>';**

The opening tag for the "previous" link.

**$config['prev_tag_close'] = '</div>';**

The closing tag for the "previous" link.

***********************************
Customizing the "Current Page" Link
***********************************

**$config['cur_tag_open'] = '<b>';**

The opening tag for the "current" link.

**$config['cur_tag_close'] = '</b>';**

The closing tag for the "current" link.

****************************
Customizing the "Digit" Link
****************************

**$config['num_tag_open'] = '<div>';**

The opening tag for the "digit" link.

**$config['num_tag_close'] = '</div>';**

The closing tag for the "digit" link.

****************
Hiding the Pages
****************

If you wanted to not list the specific pages (for example, you only want
"next" and "previous" links), you can suppress their rendering by
adding::

	 $config['display_pages'] = FALSE;

****************************
Adding attributes to anchors
****************************

If you want to add an extra attribute to be added to every link rendered
by the pagination class, you can set them as key/value pairs in the
"attributes" config::

	// Produces: class="myclass"
	$config['attributes'] = array('class' => 'myclass');

.. note:: Usage of the old method of setting classes via "anchor_class"
	is deprecated.

*****************************
Disabling the "rel" attribute
*****************************

By default the rel attribute is dynamically generated and appended to
the appropriate anchors. If for some reason you want to turn it off,
you can pass boolean FALSE as a regular attribute

::

	$config['attributes']['rel'] = FALSE;

***************
Class Reference
***************

.. php:class:: CI_Pagination

	.. php:method:: initialize([$params = array()])

		:param	array	$params: Paramètre de configuration
		:returns: instance CI_Pagination (enchainement de méthodes)
		:rtype:	CI_Pagination

		Initialise la classe pagination avec vos paramètres de configuration. 

	.. php:method:: create_links()

		:returns:	HTML-formatted pagination
		:rtype:	chaine

		Returns a "pagination" bar, containing the generated links or an empty string if there's just a single page.