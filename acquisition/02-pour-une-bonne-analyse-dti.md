---
layout: default
title: Pour une bonne analyse DTI
---

## Pour une bonne analyse DTI

Le premier type d'analyse auquel on peut penser est le DTI et le
métriques associées telles que FA, MD (=ADC), RD etc...

J'ai lu quelque part que la FA estimée étaient dépendante de la valeur
de b utilisée à l'acquisition et qu'avec un b >1200, le modèle de
diffusion faisait que la FA estimé était biaisé (DSI Studio utilise
toutes les directions avec b < **1750** pour calculer les métriques de
DTI) De fait souvent les études avec plusieurs valeurs de b estiment la
FA avec un sous-échantillon de leur acquisition, avec leur b1000 le plus
souvent. ( Par rapport à ce biais de FA pour des valeurs de b > 1200,
voir Diffusion Kurtosis Imaging (DKI) )

Concernant les directions de diffusion, 6 suffiraient mais au moins 12,
sont recommandées.
