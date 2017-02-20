Rejoindre la partie
===================

Une fois la partie crée par l'un des participants, les autres doivent pouvoir la rejoindre:

Premièrement, on rejoint la partie, en indiquant son numéro et le pseudo que l'on souhaite, par exemple,

``r.rejoindrePartie(4488,MatthieuDevallé)``

Puis on doit se synchroniser avec les autres joueurs:

``r.top()``

On a donc le code suivant pour rejoindre une partie: 

.. code-block:: python

 r.rejoindrePartie(numéro,"pseudo")
 r.top()


**Attention: On ne reprends pas la main tant que le créateur n'a pas lui même taper r.top()**
