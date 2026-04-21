# Pour une bonne tractographie

Dans ce cas, un nombre plus important de directions est requis et
l'acquisition de plusieurs valeurs de b semble recommandé. (les
réflexions ci-dessous sont en grande partie inspirée des cours du HCP:
<https://wustl.app.box.com/s/pzbdltem3jxjs0uxhz51p3mfpd9csdt5>)

A noter : la critique lue dans DSI studio sur le choix des directions du
HCP (<https://dsi-studio.labsolver.org/doc/how_to_acquire_dmri.html>)

J'ai le souvenir d'avoir lu comme recommandations d'utiliser au moins
30 directions de diffusion à b1000, et d'utiliser d'autant plus de
directions que la sphere (correspondant à une certaine valeur de b) est
grande.

Le rationel est le suivant: De plus grandes valeurs de b permettent
d'avoir une meilleur résolution angulaire pour résoudre les croisements
de fibres, mais plus b est grand et plus le SNR est faible....

![](media/image1.png)

Voir les tests faits par le HCP:

Sotiropoulos, S. N.; Jbabdi, S.; Xu, J.; Andersson, J. L.; Moeller, S.;
Auerbach, E. J.; Glasser, M. F.; Hernandez, M.; Sapiro, G.; Jenkinson,
M.; Feinberg, D. A.; Yacoub, E.; Lenglet, C.; Van Essen, D. C.; Ugurbil,
K.; Behrens, T. E. J. Advances in Diffusion MRI Acquisition and
Processing in the Human Connectome Project. NeuroImage2013, 80,
125--143. <https://doi.org/10.1016/j.neuroimage.2013.05.057>

![](media/image2.png)