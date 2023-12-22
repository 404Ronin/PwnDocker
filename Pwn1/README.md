Privilege escalation en utilisant un docker dont les droit on mal été configurés.
Nous pouvons trouver sur internet des moyens de changer les droits de docker afin de l'utiliser sans la commande root.
Juste en utilisant la commande "docker build" ce qui n'est pas normal et pas recommander.
Le but de ce TP est donc de montrer que nous pouvons avoir accès à la machine entière à cause de ce genre de configuration "pratique": https://julienc.io/blog/utiliser_le_client_docker_sans_etre_root
Sur ce blog par exemple l'auteur prétend que le fait d'utiliser la commande sudo est une mauvaise pratique et que ça permetterait de créer des brèches sécurités dans le système.
Nous allons donc montrer ici que cette méthode permet de prendre le controle total de la machine en super utilisateur.

Tout d'abord nous allons suivre son tutoriel afin de rendre docker utilisable par un groupe docker et non plus un sudoer.

Super! Nous avons donc maintenant accès à docker sans passer par sudo!
Image

Maintenant nous allons rentrer dans le vif du sujet:
Nous allons en premier lieu localiser le socket de docker et observer ses droits:
image
Nous pouvons donc voir que les droit sont accordé au groupe docker.

Maintenant que nous savons ça, nous savons que docker est exploitable.
Nous allons donc lister les image présentes sur docker avec la commande: "docker images"
Nous allons en prendre une disponible et l'utiliser pour obtenir nos super droits d'utilisateurs.
Nous allons utiliser une ligne de commande qui permet de demander un shell root depuis le conteneur.
image
Et voilà!
Nous voilà donc root et avec des super droits utilisateur. et nous pouvons accéder au dosseir protégé.
image
