# Prétraitements

## Outils disponibles

La liste suivantes des outils disponibles pour les prétraitements n'est
pas exhaustives. A noter que plusieurs logiciels (qsiprep, MicaPipe,
dmriprep, designer..) reprennent des commandes d'autres logiciels
(MRTRix, Dipy...), ce qui permet de combiner le meilleur de chaque
logiciel et de faciliter leur utilisation. Par ailleurs, certains
programmes utilisés uniquement pour des étapes spécifiques du
prétraitement (par exemple NORDIC) ne sont mentionnés que plus loin dans
le document, à l'étape correspondante.

#### Scilpy

Outils issus du Sherbrooke Connectivity Imaging Lab (SCIL)
<https://apertureneuro.org/article/154022-tractography-analysis-with-the-scilpy-toolbox>
<https://scilpy.readthedocs.io/en/latest/>

#### Dipy

Voir documentation :
<https://docs.dipy.org/stable/examples_built/preprocessing/index.html>
Plusieurs tutorials disponibles sur le site.
Dipy permet également de faire la suite des analyses

#### Mrtrix

Voir documentation :

MRtrix propose plusieurs commandes pour faire le prétraitement standards

Des tutoriels sont disponibles:

- Tutoriel B.A.T.M.A.N.(Basic And Advanced Tractography with MRtrix for
  All Neurophiles): prétraitement et tractographie avec Mrtrix ( )

- Tutoriel Andy's Brain book: introduction à Mrtix (utilise en partie le
  tutoriel BATMAN) ( )

MRTrix permet également de faire la suite des analyses (DTI, tracto .. )

#### QSIPrep

Voir documentation :

Permet de réaliser des prétraitements standards (modulable). Il intègre
des outils de plusieurs autres logiciels (MRTrix, FSL, Dipy, DSI Studio,
...).

Informations utiles :

- Utilisation via un container (docker ou singularity)

- Les données doivent être au format BIDS en entrée mais peuvent venir
  de différents protocoles (DTI, HARDI, single shell, multi shell.. ).

- Les pré-traitement suivants sont faits : correction des mouvements de
  la tête, correction des distorsion de susceptibilité, denoising,
  recalage sur la T1w, normalisation et segmentation des tissues.

- Un rapport visuel est également produit à la fin, ce qui permet de
  réaliser un QC

- Pour que la correction de susceptibilité soit faite il est nécessaire
  d'avoir ajouté « IntendedFor » dans le json de la fmap utilisée avec
  le nom de la séquence de diffusion

#### Designer-v2

Voir documentation : <https://nyu-diffusionmri.github.io/DESIGNER-v2/>
Permet de réaliser des prétraitements standards (modulable). Plusieurs
denoising sont possibles (adaptative patching, PCA, complex dat ..).

#### dmriprep

Voir documentation : <https://www.nipreps.org/dmriprep/>

#### PreQual

Voir la documentation :

Permet de réaliser les prétraitement (avec Synb0-Disco) et propose un
rapport pour faire le QC. Utilisation via un container singularity

#### MicaPipe

Voir la documentation :

Permet de faire les prétraitement de plusieurs modalités dont la
diffusion. Utilise des commandes MRTrix et ANTs. Permet également de
faire de la tractographie en utilisant MRTrix.

## Les étapes "classiques" de prétraitement

### Denoising

Débruitage des données DWI et estimation de la carte de bruit.

**MRTrix :** Commande "dwidenoise". Le débruitage est fait en
exploitant la redondance des données dans le domaine de l'analyse en
composantes principales (Marchenko-Pastur PCA).

Attention : la version à disposition dans la dernière version de MRTrix
(3.0.8) n'est pas très à jour de la littérature. A COMPLETER

**NORDIC** : <https://github.com/SteenMoeller/NORDIC_Raw> A COMPLETER

- Il faut avoir enregistrer la phase pour utiliser NORDIC (possible de
  l'utiliser sans mais les résultats sont moins intéressants)

- Fonctionne sur des données en 4D + attention au type de données
  (utiliser plutôt mrcat de MRTrix por merger les b0 si beosin)

**Patch2Self :**
<https://docs.dipy.org/stable/examples_built/preprocessing/denoise_patch2self.html#sphx-glr-examples-built-preprocessing-denoise-patch2self-py>

### Unringing

Les artefacts de Gibbs apparaissent généralement sous la forme de
plusieurs lignes parallèles fines immédiatement adjacentes aux
interfaces à contraste élevé.

Le partial Fourier très utilisé dans les acquisitions accentue ces
artefacts (10.1002/mrm.28830 )

**MRTrix :** Commande "mrdegibbs" . La suppression de l'artefact est
faite en utilisant la méthode de décalage local des sous-voxels proposée
par Kellner et al.

**Autres :** A COMPLETER

### Correction de non linéarité des gradients

A COMPLETER

### Correction des mouvements et des distorsion dues aux inhomogénéités de champs

Pour les inhomogénéités de champs, voir le groupe d'action DeltaB0 pour
plus d'informations.

**FSL Topup et FSL Eddy** : permettent de :

- la correction des mouvement entre plusieurs volumes

- la correction des mouvement au sein d'un même volume

- la correction des distorsions dues aux courants de Foucault

- la correction des distorsions dues à la susceptibilité

- le remplacement des outliers dues aux mouvements du sujet lors de
  l'acquisition d'une même coupe (ou d'une même groupe de coupe, ie
  multiband)

**MRTrix :** la commande "dwifslpreproc" permet de lancer FSL Eddy et
FSL TOPUP. Si on souhaite que la correction des inhomogénéités de champs
soit réalisée avec TOPUP, il faut avoir une séquence avec des b=0 avec
encodage de phase inversé (soit seulement des b0 soit une séquence en
blip totale).

**SynB0DISCO** () : pour les protocoles qui n'ont pas des b=0 avec
encodage de phase inversé.

Autres infos utiles :

- La norme BIDS distingue 4 cas pour nommer les différents types de
  cartes de champs possibles (voir ). Pour certains logiciels (fMRIPrep,
  QSIPrep), il est nécessaire d'avoir ajouté dans les jsons des cartes
  de champs soit IntendedFor soit B0FieldIndentifier/ B0FieldSource pour
  que la correction soit faite. Souvent ces logiciels utilisent la
  librairie python (Susceptibility Distortion Correction workFlows) .

### Correction de biais

Correction de l'inhomogénéité du champ B1. Le but est d'améliorer
l'estimation du masque du cerveau qui sera réalisée par la suite.

Il est intéressant de faire cette correction dans les cas suivant : A
COMPLETER

**MRTrix:** dwibiascorrect ants permet d'utiliser l'algorithme N4 de
ANTs

### Masque du cerveau

**MRTrix :** dwi2mask

Attention pas toujours juste surtout au niveau de la bouche si artefact

**FSL:** bet

**Freesurfer synthstrip:**
<https://surfer.nmr.mgh.harvard.edu/docs/synthstrip/>

### Recalage dans l'espcae MNI

A COMPLETER

ANTs