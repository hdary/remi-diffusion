---
layout: default
title: Paramètres généraux
---

## Paramètres généraux 


Cette partie présentera les principaux paramètres permettant de définir une acquisition de diffusion. 



Dans l'ancien document : 
Les choix cruciaux se portent vers:

- La résolution spatiale: limite haute (à 3T): 1.25mm- 1.5mm iso (HCP - HCP lifespan) - "classiquement" : 2mm iso (UK Biobank)

- Nombre de directions et de shells: limite haute: HCP (90 x 3 shell) x2 , HCP Lifespan (92 x 2 shells) x 2, ABCD ( 6b300+15b1000+15b2000+60b3000) x 1

- Facteur multibande pour réduire le TR, mais pas trop car sinon perte de signal avec repousse T1 pas complète et courants de Foucault régules venant du TR précédent.

- accélération parallèle pour réduire le TE (gain de SNR), réduire modérément le TR et réduire les distorsions (mais dépendance aux mouvement et perte intrinsèque de signal)

- Partial Fourier pour réduire le TE et modérément le TR

- Bande passante en lecture pour obtenir l'écho spacing minimal, TE minimal et limiter les distorsions, mais en sachant que plus elle haute et plus le SNR est bas.

- Répéter les différentes directions de diffusion en encodage de phase inversé pour une meilleure correction des distorsions?

