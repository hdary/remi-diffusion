---
layout: default
title: Tutorial
actions:
  - label: Guide de contribution
    url: /tutorial/contributeur.html
    variant: primary
  - label: Notebooks
    url: /tutorial/notebooks/
---

## Tutorial

Ce point d'entrée est destiné aux utilisateurs du site. Il servira à regrouper les notebooks et les guides d'exécution pour lancer des analyses d'IRM de diffusion.

Si tu veux modifier les pages Markdown du site ou ajouter une nouvelle entrée de navigation, commence par [le guide de contribution](./contributeur.md).

## Notebooks

Le dossier [notebooks](./notebooks/) accueillera les notebooks `.ipynb` pour exécuter ou documenter des pipelines de traitement.

Les notebooks pourront couvrir, par exemple:

- la conversion et la préparation des données
- le contrôle qualité
- les prétraitements
- les modélisations DTI, DKI ou NODDI
- la tractographie
- les analyses voxel-wise

## Utilisation

Les notebooks seront pensés pour être ouverts dans VS Code avec un environnement Python adapté. La logique générale sera:

1. Ouvrir le notebook.
2. Sélectionner le bon kernel Python.
3. Exécuter les cellules dans l'ordre.
4. Sauvegarder les résultats ou figures produits.

## Ressource complémentaire

Pour les personnes qui souhaitent contribuer au contenu du site, voir [le guide de contribution](./contributeur.md).
