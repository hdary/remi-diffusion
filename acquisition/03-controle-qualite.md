# Contrôle qualité données brutes

Points à vérifier (avant tout pré-traitement) :

- « Validité » des données : volumes manquants, gradients absents ou
  incohérents...

- Paramètres d'acquisition : b-values, directions, multibande, PE
  direction, TE, TR, présence de b0 avec PE opposée ou non

- Visualisation systématique des b0 et d'un sous-ensemble de volumes DW.

- Artefacts visibles : ghosting EPI, dropout, spikes, mouvement
  intra-volume.

## Mini bibliographie, discussion et tutorials

- Discussion sur neurostars :
  <https://neurostars.org/t/automated-dwi-qc-both-raw-and-pipeline-agnostic-processed/27054>

- Tutorial : <https://www.youtube.com/watch?v=stL4GMeTC1I>

## Outils disponibles

- FSL EddyQC :
  <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/eddyqc/UsersGuide>

- MRIQC :
  <https://mriqc.readthedocs.io/en/latest/iqms/dwi.html#image-quality-metrics-for-diffusion-mri-data>

- Dmriprep or qsiprep : rapports HTML automatiques et viewer :
  <https://www.nipreps.org/dmriprep-viewer/#/>