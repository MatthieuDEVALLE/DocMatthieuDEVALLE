Les Principales Fonctions
=========================


Ici, je vais détailler l'utilisation des différentes méthodes de la class Reseau, c'est donc une partie très importante car tout le système achat/vente/prix repose la-dessus.


creerPartie(self,nom)
---------------------

Crée la partie et renvoie l’id à communiqur oralement aux autres joueurs.
Exemple:

	>>> id=r.creerPartie("MatthieuDevallé")
	>>> print(id)
	31416 #id de la partie

**"nom"** (string): nom du joueur qui crée la partie


rejoindrePartie(self,id,nom)
----------------------------
 
Permet de rejoindre la partie.

**"id"** (integer): id de la partie (donné oralement par le créateur)
**"nom"** (string): pseudo du joueur qui rejoint la partie

Renvoie : 
	- 0 si tout c'est bien passe.
	- -1 si le numero de partie n'existe pas
	- -2 si le nom de joueur est déja pris
	- -3 si la partie est déja lancée (top)
	- -4 si les types ne sont pas respectés

Exemple: 

.. code-block:: python

	r.rejoindrePartie(31416,"MatthieuDev")
	>>>0 #Forcement, ça marche


top(self)
---------

Si vous avez rejoint, attend le top depart du createur.
		
Si vous avez cree, donne le top depart aux autres.
		
Renvoie toujours 0.

Exemple: 

.. code-block:: python

	>>>r.top()


solde()
-------

Permet de voir notre porte-feuille d’actions et notre argent disponible
Renvoie un dictionnaire (string:entier).
		
Exemple:

	>>> r.solde()
	{'Apple': 100, 'Facebook': 100, 'Google': 100, 'Trydea': 100, 'euros': 1000}



operationsEnCours(self)
-----------------------

Retourne une liste d’entiers, qui correspondent aux identifiants des ordres précédemment transmis et qui ne sont pas encore terminés: on peut donc les suivre et les annuler.

Exemple:
	>>> R.operationsEnCours()
	[62098581, 20555477]

ask(self,action,prix,volume)
----------------------------

Passer un ordre d'achat.
Renvoie :
	- 0 si l'ordre a ete execute directement et que tout son volume a ete ecoule
	- -4 si les types ne sont pas respectes
	- -5 si volume <= 0
	- -6 si prix <= 0
	- -7 si vous n'avez pas assez d'argent pour acheter cette quantite (prix*volume)
	- sinon renvoie l'identifiant de l'ordre (nombre positif)
			
**"action"** (string): nom de l'action
**"prix"**(float): prix unitaire
**"volume"** (integer): nombre d'actions à acheter


Exemple: 

.. code-block:: python

	r.ask('Trydea',500,30) #On veut acheter 30 actions de Trydea à un prix unitaire de 500 euros


bid(self, action, prix, volume)
-------------------------------

Passer un ordre de vente.
Renvoie :
	- 0 si l'ordre a ete execute directement et que tout son volume a ete ecoule
	- -4 si les types ne sont pas respectes
	- -8 si volume <= 0
	- -9 si prix <= 0
	- -10 si vous n'avez pas assez d'action de type action dans votre portefeuille
	- sinon renvoie l'identifiant de l'ordre (nombre positif)

**"action"** (string): nom de l'action
**"prix"** (float): prix unitaire de l'action
**"volume"** (integer): volume d'action à vendre



Exemple: 

.. code-block:: python

	r.bid("Trydea", 50, 10)
	>>>0


achats(self, action)
--------------------

Liste tous les ordres d’achats pour tous les joueurs sur une action donnée.

Retourne:
	- -4 si l’action n’existe pas
	- une liste de tuples triée par ordre de prix avantageux sous la forme: ``(nom_acheteur, prix, volume)``
		
Exemple:
	>>> r.achats("Trydea")
	[('Matthieu', 23,15), ('Ryan',20,10), ('Paul', 17,23)]


**"action"** (string): nom de l'action






ventes(self, action)
--------------------
Liste tous les ordres de ventes ouverts de tous les utilisateurs pour une action donnee.
Renvoie une liste de tuple (nom_acheteur, prix, volume) triee par le prix le plus avantageux.
Si l'action n'existe pas renvoie -4;
		
Retourne:
	- -4 si l’action n’existe pas
	- une liste de tuples triée par ordre de prix avantageux sous la forme: C{(nom_acheteur, prix, volume)}
	
Exemple:
	>>> r.ventes('Facebook')
	[('Matthieu', 5.0, 5), ('banque', 25.0, 40000)]

**"action"** (string): nom de l'action


historiques(self, action)
-------------------------
Permet de lister tous les échanges déjà effectués sur une action.
Retourne une liste de tuples triée par ordre chronologique. Sous la forme: C{(nom_vendeur, nom_acheteur, prix, volume)}
		
Exemple:
	>>> r.historiques("Trydea")
	[('Matthieu','Mukhlis',10,10), ('Térence', 'Ryan', 15,20), ('Matthieu', 'Ryan', 20,3)]

**"action"** (string): nom de l'action


suivreOperation(self, id_ordre)
-------------------------------
Permet de voir le volume restant pour un ordre transmis précédemment.
		
Retourne:
	- 0 si l’ordre n’existe plus ou est terminé
	- 4 si les types ne sont pas respectés
	- sinon le volume restant en achat/vente.
 
**"id_ordre"** (integer): id de l'ordre
 



annulerOperation(self, id_ordre)
--------------------------------
 
Annule un ordre transmis précédemment afin de récupérer les fonds provisionnés.
		
Retourne:
	- 11 si l’ordre n’existe plus ou est termine
	- 4 si les types ne sont pas respectés
	- le volume d’action restant si c’est un ordre de vente
	- les euros dépensés si c’est ordre d’achat

**"id_ordre"** (integer): id de l'odre (récupérer à partir de la fonction operationsEnCours())

Exemple: 

.. code-block:: python

	r.annulerOrdre(31416)


fin(self)
---------
Renvoie un dictionnaire le temps restant (en s) avant la fin de la partie (string:entier). Si la partie est terminée, affiche le classement (string:liste).

Exemple:
	>>> r.fin()
	{'temps': 10} #Il reste 10 secondes avant la fin de la partie.
		
	OU
	
	>>> r.fin()
	{'classement': ['Matthieu', 'Eshamuddin','banque'], 'temps': 0} #Le classement de fin de partie.

