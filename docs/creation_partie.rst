Création d’une partie
	=====================
	
  Une fois que la connexion est effectuée, on doit pouvoir choisir entre créer une partie ou en rejoindre une (à faire vous même...).
  Pour créer une partie:
  
			>>> num_partie=r.creerPartie("monNom") #On crée la partie
			print(num_partie) #On récupère son numéro
		
On récupère le numéro afin de le transmettre oralement aux autres joueurs qui eux devront rejoindre la partie.
	
**Attention: Celui qui crée la partie n’a pas besoin de la rejoindre, il est directement considéré comme un joueur**
