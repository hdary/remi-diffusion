---
layout: default
title: Export des données de diffusion
---

## DICOM 

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
