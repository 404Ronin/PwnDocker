# Contexte

Architecture 3 tiers typique:
1. Le Front-End intéragit avec les utilisateurs.
2. Le Back-end traite la logique métier.
3. La BDD stocke les données.

Une faille de configuration réseau resterai que chacun ne puisse pas uniquement communiquer avec leur coouche adjacente.

## Configuration Docker

Voici un docker-compose.yml qui configurerait les services correctements:
services:
``` YAML
  proxy:
    build: ./proxy
    networks:
      - frontend
  app:
    build: ./app
    networks:
      - frontend
      - backend
  db:
    image: postgres
    networks:
      - backend
 
networks:
  frontend:
    driver: custom-driver-1
  backend:
    driver: custom-driver-2
    driver_opts:
      foo: "1"
      bar: "2"
```
Résultat:
1. Proxy(front-end): Accède seulement au réseau 'frontend'.
2. App(Back-end); Accède aux réseaux 'frontend' et 'backend'.
3. DB (Base de données): isolée sur le réseau ('Backend')

## Scénario d'attaque

Un développeur déploie l'application sans configurer correctement les réseaux.
Un attaquant peut alors essayer de contourner le back-end et d'attaquer directement la BDD.

## Isolation Réseau
Pour éviter ce genre d'attaques la solution serait de configurer correctement le réseau comme vu au dessus. Et non pas mettre tout les applictions sur le même réseau rendant l'attaque possible.
