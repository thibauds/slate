# Export

<aside class="warning">à définir parmi les choix suivants:</aside>

Pour que votre application ait connaissance de l'image créée, lors du clic sur le bouton export nous pouvons:

* utiliser postMessage pour envoyer l'image encodée en base64 à la fenêtre parent
* utiliser postMessage pour envoyer l'url de l'image à la fenêtre parent
* utiliser un callback défini à la configuration du script qui insère l'iframe (communication avec iframe mais implémentation "cachée")
* pas de communication au niveau client mais au niveau serveur: on appelle une url (serveur à serveur)
