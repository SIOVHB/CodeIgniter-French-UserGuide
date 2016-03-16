#####################
Modèle-Vue-Contrôleur
#####################

CodeIgniter est basé sur le motif de conception Modèle- Vue-Contrôleur. 
MVC est une approche logicielle qui sépare la logique applicative de la présentation. En pratique, cela permet que les pages web contiennent un minimum de code, car la présentation est séparée de la programmation PHP.

-  Le **Modèle** représente la structure de données. Typiquement votre modèle de classe va contenir les fonctions qui vont vous permettre de récupérer, insérer, mettre à jour les informations de votre base de données.
-  La **Vue** est l'interface utilisateur. Une vue est normalement une page web, mais avec CodeIgniter, cela peut être un fragment de la page comme une en-tête et un bas de page. Cela peut aussi être une page RSS, ou d'autres types de "pages".
-  Le **Contrôleur** sert *d'intermédiaire*, entre le Modèle , la vue, et toutes autres ressources utiles pour le traitement de la requête HTTP et de la génération de la page.

CodeIgniter est une approche assez libre pour MVC car les Modèles ne sont plus requis. 
Si vous n'avez pas besoin d'ajouter une séparation, ou si vous trouvez que la maintenance des modèles requièrent plus de complexité que vous le souhaitez, vous pouvez les ignorer et construire une application minimale utilisant les Contrôleurs et les Vues.
CodeIgniter est aussi utile pour incorporer vos propres scripts existants, ou encore développer les bibliothèques principales du système, vous permettant de travailler de la manière qui vous convient le plus.

