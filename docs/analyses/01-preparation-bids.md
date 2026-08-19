---
layout: default
title: Préparation des données - BIDS pour la diffusion
---
## Le format BIDS
Le format BIDS (Brain Imaging Data Structure) est une norme pour l'organisation et la description des données de neuro-imagerie ainsi que des résultats d'études. L'utilisation de ce format standardisé facilite la réutilisation et le partage des données.

Par ailleurs, plusieurs [logiciels](https://bids-apps.neuroimaging.io/apps/) utilisent en entrée des jeux de données au format BIDS.

Les [spécifications BIDS](https://bids-specification.readthedocs.io/en/stable/) définissent la manière dont un jeu de données doit être organisé.

## Spécificité BIDS pour la diffusion

Les spécificités BIDS pour la diffusion sont détaillées dans la [norme](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetic-resonance-imaging-data.html#diffusion-imaging-data). 

Les données de diffusion (diffusion-weigthed image (dwi) et single-band reference image (sbref) doivent être stockées dans le dossier "dwi" du participant. 

### Les informations sur les gradients (bvec/bval)

Chaque fichier NIfTI ([*_]dwi.nii.gz) doit être accompagné des fichiers [*_]dwi.bval et [*_]dwi.bvec contenant les infos sur les gradients. Les fichiers .bval indiquent la valeur du facteur de diffusion (b-value en s/mm²) appliquée à chaque volume, tandis que les fichiers .bvec indiquent la direction du gradient de diffusion (vecteur 3D) utilisée pour chaque volume.
Ces fichiers doivent être au [format FSL](https://fsl.fmrib.ox.ac.uk/fsl/docs/diffusion/index.html#diffusion-data-in-fsl). 

### Les informations recommandées dans le fichier .json

Dans le fichier .json qui accompagne le NIfTI il est recommandé d'ajouter des informations sur la direction de l'encodage de phase ([`PhaseEncodingDirection`](https://bids-specification.readthedocs.io/en/stable/glossary.html#objects.metadata.PhaseEncodingDirection)) ainsi que sur le temps total de lecture de l'espace de Fourier ([`TotalReadoutTime`](https://bids-specification.readthedocs.io/en/stable/glossary.html#objects.metadata.TotalReadoutTime)) pour faciliter la suite des traitements. 

Si la diffusion est acquise en plusieurs fois ("runs"), il est recommandé d'utiliser le label "run" dans le nom des fichiers et d'ajouter 
Il est également recommandé d'ajouter [`MultipartID`](https://bids-specification.readthedocs.io/en/stable/glossary.html#objects.metadata.MultipartID) dans le fichiers json. 

### Les cartes de champ

Les différentes cartes de champ possibles sont détaillées dans la [norme](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetic-resonance-imaging-data.html#fieldmap-data). 

Si des cartes de champ sont acquises, il faut rajouter dans le fichier .json de la carte de champ le label [IntendedFor](https://bids-specification.readthedocs.io/en/stable/glossary.html#objects.metadata.IntendedFor). 

Il faut également rajouter le label [`B0FieldIdentifier`](https://bids-specification.readthedocs.io/en/stable/glossary.html#objects.metadata.B0FieldIdentifier) et dans le fichier .json de la diffusion [B0FieldSource](https://bids-specification.readthedocs.io/en/stable/glossary.html#b0fieldsource-metadata).

## Spécificité PHILIPS
### Encodage de phase
Les fichiers DICOM de Philips indiquent l'axe de codage de phase (par exemple, antéro-postérieur [AP] ou gauche-droite [LR]), mais ne précisent pas la polarité (A→P contre P→A, ou R→L contre L→R). Le label `PhaseEncodingDirection` ne sera donc pas ajoutée automatiquement au fichier JSON BIDS via des logiciels comme dcm2niix. Il est donc nécessaire de l'ajouter manuellement si vous connaissez la direction du codage de phase (information disponible sur la console de l'IRM).

Pour une image conforme à la convention [RAS (Right-Anterior-Superior) convention](https://www.slicer.org/wiki/Coordinate_systems) :

|                           |  Philips scanner  | BIDS json |
|:-------------------------:|:----------------:|:---------:|
|A>>P (anterior-posterior)  | APA              | j-        |
|P>>A (posterior-anterior)  | APP              | j         |
|R>>L (right-left)          | RLR              | i-        |
|L>>R (left-righ)           | RLL              | i         |

### Slice timing 
Dans les séquences EPI, chaque volume 3D est acquis sous forme de séquences de coupes 2D (c'est-à-dire que les différentes coupes d'un même volume ne sont pas acquises simultanément, mais successivement). Chaque fabricant (Siemens, Philips, etc.) dispose de modes d'ordre de coupe spécifiques.

Pour les scanners Philips, les modes suivants sont possibles :

- Default = le temps d'acquisition entre coupes adjacentes est maximisé
- Ascending (FH, AP, LR) = acquisition dans un ordre linéaire du pied vers la tête, de l'antérieur vers le postérieur ou de la gauche vers la droite
- Descending (HF, PA, RL) = acquisition dans un ordre linéaire de la tête vers le pied, du postérieur vers l'antérieur ou de la droite vers la gauche
- Interleaved = l'intervalle de temps entre l'acquisition de coupes voisines est maximisé (le nombre d'entrelacements est estimé par la racine carrée du nombre de coupes, arrondie à l'entier supérieur)

Afin d'effectuer la correction du temps d'acquisition des coupes (*slice timing correction*) lors des étapes de prétraitement, vous devrez connaître l'ordre des coupes. Pour Philips le label [`SliceTiming`](https://bids-specification.readthedocs.io/en/stable/glossary.html#slicetiming-metadata) n'est pas extrait automatiquement par les logiciels de conversion. Il faut le recalculer à partir des informations suivants: mode d'acquistion (pas dans le DICOM, à récupérer à la machine), temps de répétition, nombre de coupes, facteur multiband si miltiband, nombre de packet et pour les acquisition "sparse" temps de pause entre la dernière coupe du volume et le début du suivant, en secondes.

#TODO : ajouter script permettant de le faire 

### TotalReadoutTime et EffectiveEchoSpacing

Le paramètre `TotalReadoutTime`, tel que défini dans la spécification BIDS, correspond à la durée de lecture qui aurait généré des données présentant le niveau de distorsion observé (et non à la durée réelle de la séquence de lecture). Cette information ne figure pas directement dans les fichiers DICOM Philips. Si vous utilisez dcm2niix, les champs `EstimatedTotalReadoutTime` et `EstimatedEffectiveEchoSpacing` sont renseignés dans le fichier JSON.

Pour la correction par `TOPUP` (via FSL), cette information n'est pas requise si la durée de lecture est identique pour l'image principale à corriger et pour les images servant à estimer le champ (vous pouvez par exemple utiliser la valeur 1). Toutefois, certaines applications BIDS, comme fMRIPrep, exigent cette information si des images de champ (fmap) sont utilisées.

#TODO: ajouter info pour le calcul ? 


## Spécificité SIEMENS
#TODO: ajouter info 

## Spécificité GE
#TODO: ajouter info 

## Spécificité CANON 
#TODO: ajouter info 
