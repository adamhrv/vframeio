---
status: published
display_order: 5
url: /3d-printed-data
title: 3D Printed Data
title_h1: 3D Printed Synthetic Data
published: 2021-01-23
updated: 2023-03-12
weight: 2
Summary: Enriching synthetic data with 3D printed cluster munition replicas for use in image training datasets
---

{{< titling >}}

![3D printed assembly of the 9N235/9N210 submunition used for created physical synthetic data](images/vframe-9n235-replica-3d-printed.jpg#watermark)


High-quality training data is essential for developing accurate object detection algorithms. But most publicly available datasets are too generic for application to human rights investigation and recording videos of real munitions in conflict zones can put lives at risk. To offset the challenge of sourcing training data from conflict zones, VFRAME creates 3D-printed replicas to enrich training datasets and create benchmark images.

3D-printed replicas are safe, inert, proxy objects that can be photographed and annotated in various environments for use in computer vision image training datasets. The examples on this page show the 9N235 submunition fabricated fused deposition modeling (FDM), an accessible and low-cost printing method. Minimal artifacts can be seen in the raw prints (left) while the finished parts (right) are seamless. The replica shown above was fabricated in 2021 and is based on a 3D scan of a real free-from-explosive (FFE) 9N235 submunition. Each part is accurate to within a millimeter.

![The 9N235 replica photographed with wet dirt in afternoon sunlight. This image is used for training and/or benchmarking the 9N235](images/9n235_vf_02_000068.jpg#watermark)

![9N235 replica photographed with tall grass occlusions and overcast lighting. This image is used for training and/or benchmarking the 9N235](images/9n235_vf_03_000034.jpg#watermark)

Previous attempts during 2019-2020 explored using stereolithography (SLA) resin printing. The main advantage of using SLA printers is cleaner prints with less layer lines, which means less post-processing. But SLA printers require more maintenance for the resin material, including additional UV curing and disposal of hazardous fluids. 

![Previous attempt using SLA printing to create BLU-63 cluster munition replica](images/vf-sla-prints-01.jpg#watermark)

![Previous attempt using SLA printing to create AO-2.5RT cluster munition replica](images/vf-sla-prints-03.jpg#watermark)


VFRAME has been prototype this technique since 2019 in collaboration with [Mnemonic](https://mnemonic.org), an organization dedicated to preserving evidence of atrocities and war-crimes in [Syria](https://syrianarchive.org), [Yemen](https://yemeniarchive.org), and [Sudan](https://sudanesearchive.org). Since 2022 it has been used to help train the final detection models used to locate evidence of illegal cluster munition strikes in videos from Syria and Yemen, and now also in Ukraine.


### Key Findings from Research 2019 - 2023

Printing
- Use FDM printing with PLA filament for making replicas
- Print with closest color filament match as base material
- Print at 0.2mm layer height for prototype and 0.1mm for final print
- Post-process with wet sandpaper using 100-200-400-800 for smooth surfaces
- Avoid using electric sanding with dry sandpapers as it can melt plastic
- Use primer to fill gaps in layer lines between wet sanding
- Use brush or spray painting to finalize
- Combine materials (metal screws, connectors) to add more real material texture where possible

Safety
- 3D printed replicas are safe and effective alternative to using real munitions in training datasets
- 3D printed replicas are lightweight and easily transported
- 3D printed replicas can be disassembled and safely transported to unique locations and then reassembled whereas traveling with "real" replicas can be more challenging

### Acknowledgments

First version 3D replica prints made with [FormLabs](https://formblas.com) Form 2 and Form 3 SLA resin printer in Berlin by Formlabs. Thanks to Marcelo Coelho, Jory, Luke, and Ramaine.

### Exhibitions

Thanks to Ars Electronica for including this research at its early stage in their 2019 exhbition in Linz, Austria

![Cluster munition replica prints at Ars Electronica in 2019](images/ars-electronica-vframe-2019.jpg#watermark)

### Funding

This research received partial support from [SIDA / Meedan grant](/funding/#meedan)
