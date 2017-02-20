Création d'une partie
=====================

Une fois que la connexion est effectuée, on doit pouvoir choisir entre créer une partie ou en rejoindre une (à faire vous même...).

Pour créer une partie: 

.. code-block:: python
  num_partie=r.creerPartie("monNom") #On crée la partie
  print(num_partie) #On récupère son numéro

On récupère le numéro afin de le transmettre aux autres joueurs qui eux devront rejoindre la partie.

**Celui qui crée la partie n'a pas besoin de la rejoindre, il est directement considérer comme un joueur**
