##################
Classe de courriel
##################

La classe de courriel du robuste CodeIgniter supporte les fonctionnalités
suivantes :

-  Plusieurs protocoles : Mail, Sendmail, et SMTP
-  Chiffrement avec TLS et SSL pour SMTP
-  Plusieurs destinataires
-  CC (copie à) et BCC (copie cachée à)
-  Courriels en HTML ou en texte brut
-  Pièces jointes
-  Césure des mots
-  Prioritiés
-  Envoi en gros par BCC, permettant aux grandes listes d’être découpées en
   plusieurs petits groupes.
-  Outils de déboggage pour le mail

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

*************************************
Utilisation de la biblothèque de mail
*************************************

Envoyer un mail
===============

Envoyer un mail n’est pas seulement simple, mais vous pouvez le configurer à la
volée ou spécifier les préférences dans le fichier de configuration.

Voici un exemple basique expliquant comment vous pouvez envoyer un mail. Note :
cet exemple suppose que vous envoyer le mail depuis l’un de vos
:doc:`contrôleurs <../general/controllers>`.

::

	$this->load->library('email');

	$this->email->from('vous@example.com', 'Votre nom');
	$this->email->to('quelque-un@example.com');
	$this->email->cc('un-autre@un-autre-example.com');
	$this->email->bcc('eux@leur-example.com');

	$this->email->subject('Test mail');
	$this->email->message('Essai de la classe mail.');

	$this->email->send();

Régler les préférences de mail
==============================

Il y a 21 préférences différentes disponibles pour affiner comment vos mails
seront envoyés. Autrement, vous pouvez les régler manuellement comment nous le
décrivons ici, ou automatiquement via les préférences stockées dans le fichier
de configuration, décrit ci-dessous :

Les préférences sont réglées dans un tableau de préférences où les valeurs sont
passées à la méthode d’initialisation de mail. Voici un exemple de la façon de
choisir des réglages::

	$config['protocol'] = 'sendmail';
	$config['mailpath'] = '/usr/sbin/sendmail';
	$config['charset'] = 'iso-8859-1';
	$config['wordwrap'] = TRUE;

	$this->email->initialize($config);

.. note:: La plus part des paramètres ont une valeur par défaut qui sera
        utilisée si on ne les spécifie pas.

Réglage des paramètres de mail dans un fichier de configuration
---------------------------------------------------------------

Si vous préférez ne pas régler les paramètres en utilisant la méthode suivante,
vous pouvez les mettres dans un fichier de configuration. Créeez simplement
un nouveau fichier que vous appellerez email.php, et ajoutez le tableau $config.
Puis sauvegardez le fichier sous config/email.php et il sera utilisé
automatiquement. Nous n’avez PAS besoin d’utiliser la méthode
``$this->email->initialize()`` si vous sauvegardez vos préférences dans le
fichier de configuration.

Réglages d’email
================

Voici une liste de tous les réglages que vous pouvez spécifier quand vous
envoyez un email.

=================== ====================== ============================ ================================================================================================
Réglage             Valeur par défaut      Options                      Description
=================== ====================== ============================ ================================================================================================
**useragent**       CodeIgniter            Non                          Le "user agent".
**protocol**        mail                   mail, sendmail, ou smtp      Le protocole d’envoi de mail.
**mailpath**        /usr/sbin/sendmail     Non                          Le chemin vers le serveur Sendmail.
**smtp_host**       Aucune                 Non                          L’adresse du serveur SMTP.
**smtp_user**       Aucune                 Non                          Nom d’utilisateur SMTP.
**smtp_pass**       Aucune                 Non                          Mot de passe SMTP.
**smtp_port**       25                     Non                          Port SMTP.
**smtp_timeout**    5                      Non                          Temps limite (en secondes).
**smtp_keepalive**  FALSE                  TRUE or FALSE (boolean)      Activer les connexions SMTP persistantes.
**smtp_crypto**     Aucune                 tls or ssl                   Chiffrement SMTP.
**wordwrap**        TRUE                   TRUE or FALSE (boolean)      Activer la césure de mots.
**wrapchars**       76                                                  Limite de caractères avant césure.
**mailtype**        text                   text or html                 Le type de mail. Si vous envoyez un email HTML, vous devez l’envoyer comme une page web complète.
                                                                        Prenez garde à ne pas avoir de liens ou images relatifs ou il ne vont pas fonctionner.
**charset**         ``$config['charset']``                              Encodage (utf-8, iso-8859-1, etc.).
**validate**        FALSE                  TRUE or FALSE (boolean)      Validation de l’adresse email.
**priority**        3                      1, 2, 3, 4, 5                Priorité de l’email. 1 = le plus haut. 5 = le plus faible. 3 = normal.
**crlf**            \\n                    "\\r\\n" or "\\n" or "\\r"   Caractère de nouvelle ligne. (Use "\\r\\n" to comply with RFC 822).
**newline**         \\n                    "\\r\\n" or "\\n" or "\\r"   Caractère de nouvelle ligne. (Use "\\r\\n" to comply with RFC 822).
**bcc_batch_mode**  FALSE                  TRUE or FALSE (boolean)      Activer l’envoi massif en BCC.
**bcc_batch_size**  200                    Non                          Nombre de mails dans cache envoi en BCC.
**dsn**             FALSE                  TRUE or FALSE (boolean)      Activer la notification de messages sur le serveur.
=================== ====================== ============================ ================================================================================================

Ne pas tenir compte du retour à la ligne
========================================

Si vous avez activé le retour à la ligne (ce qui est recommandé pour respecter
la RFC 822) et que vous avez un très long lien dans votre mail, il sera aussi
coupé, ce qui le rendra incliquable pour la personne qui le recevera.
CodeIgniter vous laisse la possibilité de manuellement ne pas tenir compte du
retour à la ligne comme ceci::

	Le texte de votre mail va être
	normalement coupé.

	{unwrap}http://example.com/un_long_lien_qui_ne_sera_pas_coupe.html{/unwrap}

	Plus de text qui sera aussi
	normalement coupé.


Mettez les mots que vous voulez garder d’un bloc entre : {unwrap} {/unwrap}

*******************
Classe de Réference
*******************

.. php:class:: CI_Email

	.. php:method:: from($from[, $name = ''[, $return_path = NULL]])

		:param	string	$from: "From" e-mail address
		:param	string	$name: "From" display name
		:param	string	$return_path: Optional email address to redirect undelivered e-mail to
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

		Spécifier l’adresse mail et le nom de la personne qui l’envoie::

			$this->email->from('you@example.com', 'Your Name');

		Vous pouvez aussi spécifier un Return-Path, ce qui va aider la redirection de mails non délivrés::

			$this->email->from('you@example.com', 'Your Name', 'returned_emails@example.com');

		.. note:: Return-Path ne peut pas être utilisé si vous avez configuré
			'smtp' comme protocole.

	.. php:method:: reply_to($replyto[, $name = ''])

		:param	string	$replyto: E-mail address for replies
		:param	string	$name: Display name for the reply-to e-mail address
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

		Spécifier l’adresse de réponse. Si l’information n’est pas fournie,
		la méthode :meth:from est utilisée. Éxample::

			$this->email->reply_to('you@example.com', 'Your Name');

	.. php:method:: to($to)

		:param	mixed	$to: Comma-delimited string or an array of e-mail addresses
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

		Spécifier le(s) adresse(s) mail du (des) destinataire(s). Celà peut être une adresse unique,
		ou une liste délimitée par des virgules ou un tableau::

			$this->email->to('someone@example.com');

		::

			$this->email->to('one@example.com, two@example.com, three@example.com');

		::

			$this->email->to(
				array('one@example.com', 'two@example.com', 'three@example.com')
			);

	.. php:method:: cc($cc)

		:param	mixed	$cc: Comma-delimited string or an array of e-mail addresses
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

		Spécifier les adresses de CC. Comme pour "to", peut-être une adresse unique,
		un liste délimitée par des virgules ou un tableau.

	.. php:method:: bcc($bcc[, $limit = ''])

		:param	mixed	$bcc: Comma-delimited string or an array of e-mail addresses
		:param	int	$limit: Maximum number of e-mails to send per batch
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

                Spécifier l’adresse email BCC. Tout comme la méthode ``to()``,
                cela peut-être une adresse unique, une liste délimitée par des
                virgules ou un tableau.

                Si la variable ``$limit`` est spécifiée, le « mode d’envoi en
                masse » sera activé, qui enverra les mails aux correspondants,
                où chaque correspondant ne dépassera pas la ``$limit``
                spécifiée.

	.. php:method:: subject($subject)

		:param	string	$subject: E-mail subject line
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

		Spécifier le sujet du mail::

			$this->email->subject('This is my subject');

	.. php:method:: message($body)

		:param	string	$body: E-mail message body
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

                Spécifier le corps de texte du mail::

			$this->email->message('This is my message');

	.. php:method:: set_alt_message($str)

		:param	string	$str: Alternative e-mail message body
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

                Spécifier le corps de texte alternatif::

			$this->email->set_alt_message('This is the alternative message');

                Il s’agît d’un chaîne optionnelle qui peut être utilisée si vous
                envoyez un mail formatté en HTML. Ceci vous permet de spécifier
                un message alternatif non formatté en HTML qui est ajouté au
                début du message pour les personnes qui n’acceptent pas les
                mails en HTML. Si vous ne spécifiez pas votre propre message,
                CodeIgniter extraira depuis votre mail HTML et retirera les
                balises HTML.

	.. php:method:: set_header($header, $value)

		:param	string	$header: Header name
		:param	string	$value: Header value
		:returns:	CI_Email instance (method chaining)
		:rtype: CI_Email

		Ajouter des en-têtes additionnels au mail::

			$this->email->set_header('Header1', 'Value1');
			$this->email->set_header('Header2', 'Value2');

	.. php:method:: clear([$clear_attachments = FALSE])

		:param	bool	$clear_attachments: Whether or not to clear attachments
		:returns:	CI_Email instance (method chaining)
		:rtype: CI_Email

                Initialise à zéro toutes les variables du mail. Cette méthode a
                pour but d’être utilisée si vous envoyez le mail dans une
                boucle, permettant aux données d’être réinitialisées entre
                chaque cycle.

		::

			foreach ($list as $name => $address)
			{
				$this->email->clear();

				$this->email->to($address);
				$this->email->from('your@example.com');
				$this->email->subject('Here is your info '.$name);
				$this->email->message('Hi '.$name.' Here is the info you requested.');
				$this->email->send();
			}

                Si vous spécifiez le paramètre à TRUE, chaque pièce-jointe sera
                aussi supprimée::

			$this->email->clear(TRUE);

	.. php:method:: send([$auto_clear = TRUE])

		:param	bool	$auto_clear: Whether to clear message data automatically
		:returns:	TRUE on success, FALSE on failure
		:rtype:	bool

                La méthode d’envoi de mail. Retourne un booléen TRUE ou FALSE
                basé sur le succès ou l’échec, permettant d’être utilisé
                conditionnellement::

			if ( ! $this->email->send())
			{
				// Generate error
			}

                Cette méthode effacera automatiquement tous les paramètres si la
                requête s’est bien déroulée. Pour arrêter ce comportement,
                passez FALSE comme paramètre de la fonction::

		 	if ($this->email->send(FALSE))
		 	{
		 		// Parameters won't be cleared
		 	}

		.. note:: Pour éviter l’utilisation de la méthode ``print_debugger()``, vous ne devez
			pas effacer les paramètres du mail.

	.. php:method:: attach($filename[, $disposition = ''[, $newname = NULL[, $mime = '']]])

		:param	string	$filename: File name
		:param	string	$disposition: 'disposition' of the attachment. Most
			email clients make their own decision regardless of the MIME
			specification used here. https://www.iana.org/assignments/cont-disp/cont-disp.xhtml
		:param	string	$newname: Custom file name to use in the e-mail
		:param	string	$mime: MIME type to use (useful for buffered data)
		:returns:	CI_Email instance (method chaining)
		:rtype:	CI_Email

                Vous permet d’envoyer une pièce jointe. Mettre le nom/chemin du
                fichier en premier paramètre. Pour de multiples pièces-jointes,
                utilisez la méthode plusieurs fois.
		Par exemple::

			$this->email->attach('/path/to/photo1.jpg');
			$this->email->attach('/path/to/photo2.jpg');
			$this->email->attach('/path/to/photo3.jpg');

                Pour utiliser la disposition par défaut (pièce-jointe), laissez
                le second paramètre vide, autrement utilisez une disposition
                personnalisée::

			$this->email->attach('image.jpg', 'inline');

		Vous pouvez aussi utiliser une URL::

			$this->email->attach('http://example.com/filename.pdf');

                Si vous voulez utiliser un nom de fichier particulier, vous
                pouvez utiliser le troisième paramètre::

			$this->email->attach('filename.pdf', 'attachment', 'report.pdf');

                Si vous devez utiliser une mémoire tempon à la place d’un
                fichier réel — physique — vous pouvez utiliser le premier
                paramètre comme mémoire tampon, le troisième paramètre comme nom
                de fichier et le quatrière comme mime-type::

			$this->email->attach($buffer, 'attachment', 'report.pdf', 'application/pdf');

	.. php:method:: attachment_cid($filename)

		:param	string	$filename: Existing attachment filename
		:returns:	Attachment Content-ID or FALSE if not found
		:rtype:	string
 
                Spécifie et retourne le Content-ID de la pièce jointe, qui vous
                permet d’ajouter une image dans le message HTML. Le premier
                paramètre doit être un nom de pièce-jointe.::
 
			$filename = '/img/photo1.jpg';
			$this->email->attach($filename);
			foreach ($list as $address)
			{
				$this->email->to($address);
				$cid = $this->email->attachment_cid($filename);
				$this->email->message('<img src='cid:". $cid ."' alt="photo1" />');
				$this->email->send();
			}

		.. note:: Content-ID for each e-mail must be re-created for it to be unique.

	.. php:method:: print_debugger([$include = array('headers', 'subject', 'body')])

		:param	array	$include: Which parts of the message to print out
		:returns:	Formatted debug data
		:rtype:	string

                Retourne une chaîne de caractères contenant tous les messages du
                serveur, les en-têtes, et le contenu des messages. C’est très
                utile pour débugguer.

                Optionnellement, vous pouvez spécifier quelles parties du
                message devront être imprimées.
		Les options valides sont : **headers**, **subject**, **body**.

		Exemple::

			// You need to pass FALSE while sending in order for the email data
			// to not be cleared - if that happens, print_debugger() would have
			// nothing to output.
			$this->email->send(FALSE);

			// Will only print the email headers, excluding the message subject and body
			$this->email->print_debugger(array('headers'));

		.. note:: By default, all of the raw data will be printed.
