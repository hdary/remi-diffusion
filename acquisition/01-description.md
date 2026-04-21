---
layout: default
title: Description
---

## Bonnes pratiques pour l'IRM de diffusion en neuro

## Groupe d'actions du REMI

## Description

## Responsables

Julien Lamy, Bixente Dilharreguy, Clément Debacker, Bastien Cagna,
Jean-Luc Anton, Marie Chupin, Hugo Dary, Franck Lamberton, Julien Sein,
Arnaud LeTroter, Romain Valabrègue, Romain Viard, Emmanuelle Gourieux

## Objectifs

Établir des bonnes pratiques d'acquisition et de traitement

### Court terme

exploitation des informations de diffusion depuis les fichiers DICOM

### Long terme

Bonnes pratiques d'acquisition et de traitement (incluant
recommandations, tutoriel et pipeline de traitement) en DTI et en NODDI

Définir des mesures de qualité des données et de certains types de
résultats

Tester sur des données communes différentes chaînes de pré-traitement

Émettre des recommandations sur les paramètres des acquisitions et les
pré-traitements à mettre en œuvre

Proposer une chaîne de traitement REMI à l'état de l'art et didactique:
script bash, jupyter notebook, ...

## Livrables

Exploitation des informations de diffusion depuis les fichiers DICOM :
comment les directions de diffusion et les b-valeurs sont-elles stockées
dans les fichiers DICOM ?

Une bibliographie structurée et partagée avec zotero:
<https://www.zotero.org/groups/4555775/remi_diffusion>

Lister, pour chaque plateforme/équipe intéressée, les paramètres des
acquisitions utilisées en routine et les pré-traitements couramment mis
en œuvre :
<https://docs.google.com/spreadsheets/d/1vpAtnPMVdDaplYqw-LtMdrbt_VEKoWKpJtNG79KqFxw/edit#gid=0>

Éventuellement lister également les questions souvent abordées en
Neurosciences.

## Protocole(s) de Diffusion idéal (aux)?

L'idée est ici de réfléchir à un protocole "standard" (à 3T pour le
moment mais des discussions pour les autres champs peuvent être
discutées aussi!) qui peut être proposé par le REMI, en compilant
l'expérience des uns et des autres. Un exemple de pipeline permettant
d'obtenir des résultats pourrait aussi y être associé.

Le titre est volontairement provocateur car un tel protocole n'existe
pas, vu la multitude de modèle existant actuellement dans la
littérature, et les contraintes diverses et variées liées à chaque
étude.

Nous pouvons essayer de résumé ici les contributions de chacun et ce
sujet et voir si on converge vers un protocole?

Pour information, voici un récapitulatif de quelques protocoles utilisés
ici et ailleurs:
<https://docs.google.com/spreadsheets/d/1vpAtnPMVdDaplYqw-LtMdrbt_VEKoWKpJtNG79KqFxw/edit#gid=0>

Les choix cruciaux se portent vers:

- La résolution spatiale: limite haute (à 3T): 1.25mm- 1.5mm iso (HCP -
  HCP lifespan) - "classiquement" : 2mm iso (UK Biobank)

- Nombre de directions et de shells: limite haute: HCP (90 x 3 shell) x2
  , HCP Lifespan (92 x 2 shells) x 2, ABCD (
  6b300+15b1000+15b2000+60b3000) x 1

- Facteur multibande pour réduire le TR, mais pas trop car sinon perte
  de signal avec repousse T1 pas complète et courants de Foucault
  régules venant du TR précédent.

- accélération parallèle pour réduire le TE (gain de SNR), réduire
  modérément le TR et réduire les distorsions (mais dépendance aux
  mouvement et perte intrinsèque de signal)

- Partial Fourier pour réduire le TE et modérément le TR

- Bande passante en lecture pour obtenir l'écho spacing minimal, TE
  minimal et limiter les distorsions, mais en sachant que plus elle
  haute et plus le SNR est bas.

- Répéter les différentes directions de diffusion en encodage de phase
  inversé pour une meilleure correction des distorsions?

Le site de DSI-Studio propose et discute un protocole « idéal » à 23
valeurs de b et 258
directions (<https://dsi-studio.labsolver.org/doc/how_to_acquire_dmri.html>).
La comparaison de l'encodage type q-space versus un multi-shell plus
classique est intéressante, notamment le besoin de redondance dans les
valeurs de b acquises pour interpoler les données manquantes au moment
de la correction par « eddy ».

=> il faut bien noter les avantages et inconvénients de cette méthode
et le fait qu'il faut notamment acquérir avec les gradients de diffusion
en mode dipolaire et que ce type d'acquisition ne convient pas à une
reconstruction de type CSD.
