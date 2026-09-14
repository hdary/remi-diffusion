---
layout: default
title: Paramètres généraux
---

## Paramètres généraux 


Cette partie présentera les principaux paramètres permettant de définir une acquisition de diffusion. 

Description des différentes séquences et nom constructeurs ?

Dans l'ancien document : 

Les choix cruciaux se portent vers:

- La résolution spatiale: limite haute (à 3T): 1.25mm- 1.5mm iso (HCP - HCP lifespan) - "classiquement" : 2mm iso (UK Biobank)

- Nombre de directions et de shells: limite haute: HCP (90 x 3 shell) x2 , HCP Lifespan (92 x 2 shells) x 2, ABCD ( 6b300+15b1000+15b2000+60b3000) x 1

- Facteur multibande pour réduire le TR, mais pas trop car sinon perte de signal avec repousse T1 pas complète et courants de Foucault régules venant du TR précédent.

- accélération parallèle pour réduire le TE (gain de SNR), réduire modérément le TR et réduire les distorsions (mais dépendance aux mouvement et perte intrinsèque de signal)

- Partial Fourier pour réduire le TE et modérément le TR




## Temps de répétition

## Multi-bande et/ou Grappa

## Gradient mono ou bi-polaire

## Acquisitions segmentées

## Transformée de fourier partielles

Impact sur les analyses ?

## Résolution

Rorden conseille du 3 mm iso. Ca parait être une résolution peu basse et
on risque d'y perdre en résolution angulaire ; si le temps le permet, 2
mm iso ou moins) serait plus adapté. La résolution isotrope est en
revanche très importante : sans ça on aura une atténuation différente
selon l'orientation relative des structures, du voxel, et du gradient
de diffusion.

## b-valeurs

en plus d'une acquisition à b=0 s/mm^2, il serait intéressant de faire
les acquisitions à deux b-valeurs (e.g. 750 s/mm^2 et 1000 s/mm^2)
afin de mieux identifier le champ contenant cette valeur et les
éventuelles variations liées au stockage soit de la b-valeur idéale
(telle que saisie sur la console) ou de la b-valeur effective (modulée
par les gradients d'imagerie).

## Directions du gradient de diffusion

12 directions suffisent, si elles sont bien échantillonnées. Si on
utilise les deux b-valeurs précédentes, on peut utiliser 12 directions
pour b=1000 s/mm^2 et 9 pour b=750 s/mm^2.

## Orientation des coupes

plusieurs acquisitions avec des orientations de coupes différentes
doivent être réalisés afin de déterminer le repère utilisé par les
directions du gradient de diffusion (patient, aimant, gradient, image,
etc.). On peut s'en sortir a minima avec trois acquisitions, en axial
pur, sagittal pur, coronal pur. Rorden conseille en plus de rajouter une
orientation oblique à 30 °, et il peut être intéressant de jouer
également avec les directions respectives des gradients de lecture et de
phase (e.g. acquisitions axiales avec lecture en RL et phase en AP puis
lecture en AP et phase en RL).


- Bande passante en lecture pour obtenir l'écho spacing minimal, TE minimal et limiter les distorsions, mais en sachant que plus elle haute et plus le SNR est bas.

- Répéter les différentes directions de diffusion en encodage de phase inversé pour une meilleure correction des distorsions?

