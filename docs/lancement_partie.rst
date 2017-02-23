Synchronisation pour le départ
==============================

Lorsque tous les utilisateurs ont rejoint la partie, il faut se synchroniser pour le top depart.
Pour cela, ceux qui ont rejoint la partie utiliseront :
  
			>>> r.top() #ne rend pas la main tant que le createur n'a pas lance
		
Une fois que tous les joueurs ont rejoint la partie, le créateur entre à son tour qui lance la partie:
A partir de la, createur et utilisateurs ont acces aux memes fonctions du jeu.

			>>> r.solde()
			{'Apple': 100, 'Facebook': 100, 'Google': 100, 'Trydea': 100, 'euros': 1000}
	
A partir de ce moment, il n’y a plus de différence entre le créateur et les autres.
