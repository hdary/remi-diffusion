---
layout: default
title: Modélisations
---

## Modélisations

Les explications données dans cette parties sont partielles et la liste
des outils disponibles n'est pas exhaustive.

## Diffusion Tensor Imaging (DTI)

#### Mini bibliographie :

- Basser PJ, Mattiello J, LeBihan D. Estimation of the effective
  selfdiffusion tensor from the NMR spin echo. J Magn Reson B 1994;103:
  247-254.

- Horsfield MA, Jones DK. Applications of diffusion-weighted and
  diffusion tensor MRI to white matter diseases --- A review. NMR Biomed
  2002;15:570-577

#### Explications (partielles):

Le tenseur de diffusion (DT) décrit la diffusion des molécules d'eau à
l'aide d'un modèle gaussien et a pour but de caractériser la diffusion
(coefficient d'anisotropie, directions privilégiées dans l'espace ..).
Le DTI est basé sur l'hypothèse que la diffusion des particules d'eau
dans la microstructure des tissus suit une distribution gaussienne, ce
qui est le cas dans les régions où les faisceaux de fibres sont
« cohérents »

On peut extraire du DTI plusieurs métriques quantitatifs :

- Fractional Anisotropy (FA) : décrit la quantité de diffusion qui est
  anisotrope et montre donc la direction privilégiée de la diffusion

- Mean Diffusivity (MD) = Apparrent Diffusion Coefficient (ADC) :
  diffusion moyenne

- Axial Diffusivity (AD) : diffusion dans la direction axiale

- Radial Diffusivity (RD) : diffusion dans la direction radiale
  (perpendiculaire à la diffusion axiale)

- Trace : sommes des valeurs propres du tenseur

- FA color

Le DTI est très utile en clinique.

Remarques en vrac:

- Il faut au moins 6 directions pour obtenir un tenseur de diffusion

- Dans les zones où l'hétérogénéité des tissus est importantes (cortex
  cérébral par ex où il y a beaucoup de fibres qui se croisent), le
  comportement de la diffusion de l'eau dans les tissus s'écarte du
  comportement gaussien supposé, il est donc difficile d'interpréter les
  paramètres dérivées du DTI

AJOUTER DES RESSOURCES + IMAGES

#### Outils disponibles

##### MRTrix

Il est possible d'obtenir le DTI avec MRTrix via la commande puis
d'obtenir les métriques avec la commande .

##### FSL

FSL permet d'obtenir le DTI et d'obtenir les métriques avec la commande

## Diffusion Kurtosis Imaging (DKI)

#### Mini bibliographie:

- Papiers « originaux » :

> Jensen JH « Diffusional Kurtosis Imaging: The Quantification of Non-
> Gaussian Water Diffusion by Means of Magnetic Resonance
> Imaging » ;Magn Reson Med 2005; (1er papier sur le DKI)
>
> Jensen JH « MRI Quantification of Non-Gaussian Water Diffusion by
> Kurtosis Analysis » ; NMR Biomed. 2010

- Reproductibilité :

> Loxlan W. Kasa « Evaluating High Spatial Resolution Diffusion Kurtosis
> Imaging at 3T: Reproducibility and Quality of Fit » ; Magn Reson Med
> 2021

- Autres :

#### Explications (partielles):

Le modèle DTI suppose que la diffusion des molécules d'eau suit une
distribution Gaussienne. Cette hypothèse est incorrecte pour les tissus
biologiques complexes. Ce comportement non gaussien est encore plus
important pour des gradients forts (si on augmente les valeurs de b)
et/ou si on utilise un temps d'écho long.

Le paramètre statistique "Kurtosis" (K) est égale à 0 dans le cas d'une
distribution gaussienne. Pour la diffusion de l'eau dans les tissus
biologique on a K>0.

Le modèle du DKI est une extension du modèle DTI qui permet de mieux
quantifier le degré de "non-gaussianité" de la diffusion de l'eau à
l'aide du tenseur de kurtosis (KT).

Pourquoi utiliser le DKI ?

- Caractériser l'hétérogénéité de la microstructure des tissus

- Obtenir des des paramètres biophysiques comme la densité des fibres
  axonales

Le DKI permet d'obtenir les cartes "classiques" du modèle DTI (FA,
MD..). Ces cartes sont similaires à celles obtenues avec le DTI (mais
pas exactement égales). On obtient d'autres cartes spécifiques au DKI.
Les cartes suivantes dépendent à la fois du tenseur de diffusion et du
tenseur du Kurtosis :

- Mean kurtosis (MK) (plus important dans la WM car plus compartimentée)

- Axial Kurtosi (AK)

- Radial Kurtosis (RK) (avec des valeurs normalement plus important que
  le AK car le comportement non-Gaussien est censé être plus important
  perpendiculairement aux fibres de WM)

Les cartes suivantes dépendent seulement du tenseur de kurtosis :

- Mean of the Kurtosis tensor (MKT) (similaire au MK)

- Kurtosis fractional anisotropy (KFA)

Ces différentes mesures dépendent des propriétés microstructurelles et
des propriétés mésoscopiques (dispersions des fibres, intersection des
fibres).

Remarques en vrac:

- Pour faire du DKI il est nécessaire d'avoir des données multi-shell
  (au moins 2 shell en plus des b=0 s/mm²) et d'avoir au moins 15
  directions de diffusion différentes.

- Les effets de la diffusion Kurtosis sont plus visibles pour les
  valeurs de b > 1500 s/mm²

- Valeurs habituelles de K dans le cerveau : CSF~0, GM~0.7, WM~1

- Le DKI est sensible aux bruits et aux artefacts. Par ex il peut être
  mal estimé et avoir des valeurs impossibles/ négatives dans les
  régions où la diffusivité radiale est faible

- Constrained optimization for DKI : pour éviter les valeurs de DKI
  physiquement impossibles on peut utiliser un fit contraint pour
  l'estimation du DKI ()

- Mean signal diffusion kurtosis imaging (MSDKI) : une autre méthode
  consiste à caractériser le kurtosis à partir des signaux moyens des
  données acquises dans toutes les directions pour chaque valeur de b =
  (powder-averaged signals) afin de limiter la sensibilité au bruit et
  aux artefacts. Les cartes obtenues dans ce cas ne dépend pas de la
  distribution des fibres ()

#### Outils disponibles

##### FSL

L'outil « **dtifit** » a une option pour calculer les paramètres de
kurtosis :

**--kurt** Output mean kurtosis map (for multi-shell data)

**--kurtdir** Output maps of kurtosis along each eigenvector: K1, K2,
and K3 (for multi-shell data)

#### Dipy

La librairie python Dipy permet de facilement estimer le DKI et
d'obtenir les cartes. Plusieurs tutoriels sont disponibles :

- 
- 

#### Diffusion Kurtosis Estimator (DKE)

Logiciel pour estimer le DKI (dernière MAJ en 2015)

- 
- 

##### DKI matlab (CAIR)

Toolboxe/ code matlab pour l'estimation du DKI

##### MRTrix

Il est possible d'obtenir le DKI avec MRTrix via la commande et l'option
--dkt .
Dans la futur version (actuellement en version dev) il sera possible
d'obtenir les cartes dérivées du DKI avec la commande (mais pas possible
actuellement, il faut revenir aux définitions des cartes et les calculer
à partir du tenseur obtenu ...)

## Neurite Orientation Dispersion and Density Imaging (NODDI)

#### Mini bibliographie

- Papier original :
  Zhang, H., 2012. NODDI: practical in vivo neurite orientation
  dispersion and density imaging of the human brain. Neuroimage 61,
  1000--1016.

- Les applications de la NODDI en recherche clinique :
  Kamiya, Kouhei . "NODDI in Clinical Research." *Journal of
  Neuroscience Methods* 346 (December 2020): 108908. .

- Reproductibilité :
  Andica, C., 2019b. Scan-rescan and inter-vendor reproducibility of
  neurite orientation dispersion and density imaging metrics.
  Neuroradiology.
  
  Chung, A.W., Seunarine, K.K., Clark, C.A., 2016. NODDI reproducibility
  and variability with magnetic field strength: a comparison between 1.5
  T and 3 T. Hum. Brain Mapp. 37, 4550--4565.

#### Explications (partielles)

Il y a 2 approches possibles pour extraire des informations des données
de diffusion. Les approches « représentation de signaux » fournissent
des statistiques sur le signal observé sans s'appuyer sur des
hypothèses concernant les tissus (DTI, DKI..). Les approches « modèles
biophysiques » paramétrisent le signal de diffusion IRM comme une
fonction des paramètres biophysiques significatifs comme la densité des
axones.

La NODDI (Neurite Orientation Dispersion and Density Imaging) est un
modèle biophysique qui doit permettre d'obtenir des marqueurs sur la
microstructure du tissue du cerveau plus spécifiques que ceux obtenus
avec des marqueurs plus classiques comme la FA.

La NODDI permet de caractérisé la microstructure à l'intérieur d'un
voxel en fournissant des informations sur la densité de neurites et sur
la dispersion de l'orientation grâce à 3 paramètres

-  intra-cellular volume fraction (ICVF) = neurite density index (NDI) :
  quantifie la densité d'empilement des neurites / estime la fraction de
  volume des neurites

- Orientation dispersion index (ODI) : estime la variabilité de
  l'orientation des neurites (de 0 à 1 avec 0 = tous parfaitement
  alignés et 1 = complètement isotrope)

- Free water fraction (FWF) : permet d'estimer l'étendue de la
  contamination du LCR.

![NODDI](../media/NODDI_model.jpg)

Figure provenant de l'article .

Autres informations :

- Le modèle NODDI assume que la diffusion suit une distribution
  Gaussienne

- Lors du développement du cerveau on observe une augmentation de la
  dispersion de l'orientation des neurites

- La répétabilité entre 2 acquisitions (inter-scanner) a été démontrée
  dans plusieurs articles sur le même IRM mais grosse différence entre
  3T et 1.5T + la reproductibilité inter-scanner est plus faible que la
  reproductibilité inter-scanner

- Utilisation possible de « tissue-weighted means » pour réduire le
  biais (article de Parker et al., 2021
  [[10.1016/j.neuroimage.2021.118749]{.underline}](http://doi.org/10.1016/j.neuroimage.2021.118749)
  )

La validité des hypothèses du modèle est en débat au sein de la
communauté. Exemple de ce qui est débattu :

- le nombre de compartiment (intra-neutrite, extra-neutrite, free water)

- le fait que la distribution de la diffusion suit une loi gaussienne
  (et qu'on néglige donc les échanges entre les compartiments et les
  effets non-gaussien dans chaque compartiment)

- le fait d'avoir fixé et contraint certains paramètres du modèle. Par
  exemple le fait d'avoir fixé la diffusivité parallèle alors qu'elle
  peut être différente en fonction de la population (enfant ou adulte)
  et en focntion du mileu (WM ou GM)

Cependant, il a été montré que la NODDI est plus spécifique que la FA et
la NODDI peut fournir des biomarqueurs utiles surtout si l'effet de la
maladie est plus important que les biais introduits.

#### Outils disponibles

##### « Original » NODDI Matlab toolbox

Code matlab :

Implémentation de l'article original de Zhang. Assez long à tourner

##### AMICO (Accelerated Microstructure Imaging via Convex Optimization)

Paquet python :

Implémentation comme décrit dans l'article : Daducci, A.,
Canales-Rodríguez, E.J., Zhang, H., Dyrby, T.B., Alexander, D.C.,
Thiran, J.P., 2015. Accelerated microstructure imaging via Convex
Optimization (AMICO) from diffusion MRI data. Neuroimage 105, 32--44.
https://doi.org/10.1016/j. neuroimage.2014.10.026

##### cuDIMOT

Toolboxe de FSL / Besoin d'avoir une carte NVIDIA GPU et CUDA
d'installer

Implémentation comme décrit dans l'article : Hernandez-Fernandez M.,
Reguly I., Jbabdi S, Giles M, Smith S., Sotiropoulos S.N. "Using GPUs to
accelerate computational diffusion MRI: From microstructure estimation
to tractography and connectomes."NeuroImage 188 (2019): 598-615.

##### MDT

Paquet python :

## SANDI

Modèle adapté au gris. Attention à ne pas l'utiliser pour le blanc.

A COMPLETER

## Autres modèles

HARDI, CHARMED .., SMT

À compléter
