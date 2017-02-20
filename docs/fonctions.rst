Les Principales Fonctions
=========================


Ici, je vais détailler l'utilisation des différentes méthodes de la class Reseau, c'est donc une partie très importante car tout le système achat/vente/prix repose la-dessus.


creerPartie(self,nom)
---------------------


Crée la partie et renvoie l'id a communiqué oralement aux autres joueurs.

**"nom"** (string): nom du joueur qui crée la partie

Exemple: 

.. code-block:: python

	id=r.creerPartie("MatthieuDevallé")
	print(id)
	>>> 31416 #id de la partie


rejoindrePartie(self,id,nom)
----------------------------
 
Permet de rejoindre la partie.

**"id"** (integer): id de la partie (donné oralement par le créateur)
**"nom"** (string): pseudo du joueur qui rejoint la partie

Retourne:
  - 0 si tout c'est bien passe
  - 1 si le numero de partie n'existe pas
  - 2 si le nom de joueur est deja pris
  - 3 si la partie est deja lance (top)
  - 4 si les types ne sont pas respecte

Exemple: 

.. code-block:: python

	r.rejoindrePartie(31416,"MatthieuDev")
	>>>0 #Forcement, ça marche


top(self)
---------

Deux possibilités:
  - si vous avez rejoint la partie, attend le top du créateur
  - si vous avez créé, lance la partie

Exemple: 

.. code-block:: python

	>>>r.top()


solde()
-------

Permet de voir notre prote-feuille d'actions et notre argent disponible

Exemple: 

.. code-block:: python

	r.solde()
	>>> {'Apple': 100, 'Facebook': 100, 'Google': 100, 'Trydea': 100, 'euros': 1000}


operationsEnCours(self)
-----------------------
 
Retroune une liste d'entier, qui correspondent aux identifiants des ordres précédements transmis et qui ne sont pas encore terminer: on peut donc les suivres et les annuler.

Exemple: 

.. code-block:: python

	r.rejoindrePartie(31416,"MatthieuDev")
	>>>0 #Forcement, ça marche

ask(self,action,prix,volume)
----------------------------

Méthode permettant de passer un ordre d'achat.

**"action"** (string): nom de l'action
**"prix"**(float): prix unitaire
**"volume"** (integer): nombre d'actions à acheter

Retourne:

  - 0 si l'ordre a été exécuté directement et que tout son volume a été écoulé
  - 4 si les types ne sont pas respectés
  - 5 si volume <= 0
  - 6 si prix <= 0
  - 7 si vous n'avez pas assez d'argent pour acheter cette quantité (prix*volume)
  - sinon renvoie l'identifiant de l'ordre (nombre positif)

Exemple: 

.. code-block:: python

	r.ask('Trydea',500,30) #On veut acheter 30 actions de Trydea à un prix unitaire de 500 euros


bid(self, action, prix, volume)
-------------------------------

Permet de passer un ordre de vente.

**"action"** (string): nom de l'action
**"prix"** (float): prix unitaire de l'action
**"volume"** (integer): volume d'action à vendre

Retourne:
  - 0 si l'ordre a été executé directement et que tout son volume a été écoulé
  - 4 si les types ne sont pas respectés
  - 8 si volume <= 0
  - 9 si prix <= 0
  - 10 si vous n'avez pas assez d'action de ce type dans votre portefeuille
  - sinon renvoie l'identifiant de l'ordre (nombre positif)

Exemple: 

.. code-block:: python

	r.bid("Trydea", 50, 10)
	>>>0


achats(self, action)
--------------------

Liste tous les ordres d'achats pour tous les joueurs sur une action donnée.

**"action"** (string): nom de l'action

Retourne:
  - -4 si l'action n'existe pas
  - une liste de tuples triée par ordre de prix avantageux sous la forme:

``(nom_acheteur, prix, volume)``

Exemple:

.. code-block:: python

	r.ventes("Trydea")
	>>> [(Matthieu, 23,15), (Ryan,20,10), (Paul, 17,23)]

ventes(self, action)
--------------------

Liste tous les ordres de ventes pour tous les joueurs sur une action donnée.

**"action"** (string): nom de l'action

Retourne:
  - -4 si l'action n'existe pas
  - une liste de tuples triée par ordre de prix avantageux sous la forme:

``(nom_acheteur, prix, volume)``

Exemple: 

.. code-block:: python

	r.ventes("Trydea")
	>>> [(Matthieu,10,15), (Mukhlis,12,10),(Paul, 15,23)]

historiques(self, action)
-------------------------

Permet de lister tous les échanges déjà effectuer sur une actions.

Retourne une liste de tuples trier par ordre chronologique. Sous la forme:
``(nom_vendeur, nom_acheteur, prix, volume)``

**"action"** (string): nom de l'action

Exemple: 

.. code-block:: python

	r.historiques("Trydea")
	>>> [(Matthieu,Mukhlis,10,10), (Térence, Ryan, 15,20), (Matthieu, Ryan, 20,3)]

suivreOperation(self, id_ordre)
-------------------------------
 
Permet de voir le volume restant pour un ordre transmis précédement.
 
**"id_ordre"** (integer): id de l'ordre
 
Retourne:
  - 0 si l'ordre n'existe plus ou est terminé
  - 4 si les types ne sont pas respectés
  - sinon le volume restant en achat/vente.

Exemple: 

.. code-block:: python

	r.suivreOperation(31416)
	>>> 10


annulerOperation(self, id_ordre)
--------------------------------
 
Annule un ordre transmis précédemment afin de récupérer les fonds provisionnés.

Retourne:
  - 11 si l'ordre n'existe plus ou est termine
  - 4 si les types ne sont pas respectes
  - le volume d'action restant si c'est un ordre de vente
  - les euros dépensés si c'est ordre d'achat

**"id_ordre"** (integer): id de l'odre (récupérer à partir de la fonction operationsEnCours())

Exemple: 

.. code-block:: python

	r.annulerOrdre(31416)


fin(self)
---------

Renvoie un dictionnaire le temps restant (en s) avant la fin de la partie (string:entier). Si la partie est terminé, affiche le classement (string:liste).

Exemple:

.. code-block:: python

	r.fin()
	>>>{10} #Il reste 10 secondes avant la fin de la partie.

.. code-block:: python

	r.fin()
	>>> {Devallé, Benkhedda, Eshamuddin} #Le classement de fin de partie

