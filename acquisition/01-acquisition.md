# Acquisition

Proposition de protocole d'acquisition, basé sur
https://github.com/neurolabusc/dcm_qa_toshiba.

L'idée est d'obtenir un protocole assez facile à mettre en place et
rapide pour déterminer comment les b-valeurs et les directions du
gradient de diffusion sont stockées dans les fichiers DICOM. En
l'absence de fantôme anisotrope facile à réaliser, il faudrait réaliser
les acquisitions sur un volontaire.

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

## Sauvegarde des images de phases

Pour utiliser NORDIC par exemple :
[https://www.sciencedirect.com/science/article/pii/S1053811920310247sdf](https://www.sciencedirect.com/science/article/pii/S1053811920310247)

Mais la question demeure sur la manière de reconstruire la phase. Les
papiers utilisant NORDIC semblent reconstruire la phase à leur façon.
Par exemple:
« In order to allow distortion correction and processing for complex
data and avoid phase incoherence artifacts, the raw complex-valued
diffusion data were rotated to the real axis using the phase
information. A spatially varying phase-field was estimated and complex
vectors were multiplied with the conjugate of the phase. The phase-field
was estimated uniquely for each slice and volume by firstly removing the
phase variations from k-space sampling and coil sensitivity combination,
and secondly by removing an estimate of a smooth residual phase-field.
The smooth residual phase-field was estimated using a low-pass filter
with a narrowed tapered cosine filter (a Tukey filter with an FWHM of
58%). Hence, the final signal was rotated approximately along the real
axis, subject to the smoothness constraints. »
Manzano-Patron, J.-P.; Moeller, S.; Andersson, J. L. R.; Yacoub, E.;
Sotiropoulos, S. N. ***Denoising Diffusion MRI: Considerations and
Implications for Analysis*;** preprint; Neuroscience,
2023. [[https://doi.org/10.1101/2023.07.24.550348]{.underline}](https://doi.org/10.1101/2023.07.24.550348).

Code de ce papier qui détaille la préparation de la phase et différentes
méthodes de denoising
<https://github.com/SPMIC-UoN/EDDEN>
Manzano Patron, J. P.; Moeller, S.; Andersson, J. L. R.; Ugurbil, K.;
Yacoub, E.; Sotiropoulos, S. N. Denoising Diffusion MRI: Considerations
and Implications for Analysis. *Imaging Neuroscience* **2024**, *2*,
1--29. [[https://doi.org/10.1162/imag_a_00060]{.underline}](https://doi.org/10.1162/imag_a_00060).

Utilisation de la phase pour le denoising avec MRTrix (fonction
dwidenoise) également : deux discussions intéressantes:
<https://github.com/PennLINC/qsiprep/issues/677>
<https://community.mrtrix.org/t/unwrapping-before-dwidenoise-on-complex-valued-data/4039>

## 3D-SE-EPI

Nouvelles séquences ou reconstructions fournies par les constructeurs?
(AP et PA simultanées?)

Rq : AP et PA simultanée disponible chez Siemens en C2P pour XA (en 2D
SE-EPI) :
Afacan, O.; Hoge, W. S.; Wallace, T. E.; Gholipour, A.; Kurugol, S.;
Warfield, S. K. **Simultaneous Motion and Distortion Correction Using
Dual-Echo Diffusion-Weighted MRI.** Journal of
Neuroimaging 2020, 30 (3),
276--285. [[https://doi.org/10.1111/jon.12708]{.underline}](https://doi.org/10.1111/jon.12708).

# Traitement de données :

voir ici
https://resana.numerique.gouv.fr/public/perimetre/consulter/532839?information=44532971