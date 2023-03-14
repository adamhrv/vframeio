---
title: 9N235
description: Building 9N235/210 submunition object detector
url: /9n235
date: 2023-03-01
Tags: ['cluster munition', 'submunition', '9N235', '9N210']
images:
- https://vframe.io/9n235/images/vframe_t4t_9n235_photogrammetry.png
---

# 9N235/9N210 Submunition Object Detector

Building a 9N235/210 submunition object detector with photography, photogrammetry, 3D-rendering, 3D-printing, and convolutional neural networks

<small><i class="fa fa-hammer" aria-hidden="true"></i> This page is still under development and comprises the preliminary version of a research report to be submitted in the next few months.</small>

![Example detection performance on partially exploded 9N235/9N210 submunition recovered by Ukrainian forces after a Russian attack. Detection made using VFRAME&rsquo;s open-source 9N235/9N210 detector model. Munition accessed in collaboration with Tech 4 Tracing.](images/detections/20230214_vf_9n235_facility_i_015_crop.jpg#watermark)

This page outlines the development process of building an object detector for the 9N235/210 submunition using photography, photogrammetry, 3D modeling, 3D printing, and convolutional neural networks. For code and models visit [github.com/vframeio/vframe](https://github.com/vframeio/vframe). The model is free to use for commercial purposes if the LICENSE and CREDIT information is included (MIT).

Updates:
- February 2023: Improved detection models (v0.2) released
- October 2022:  VFRAME partner Tech 4 Tracking dispatches [policy brief (PDF)](https://tech4tracing.org/wp-content/uploads/2022/08/T4T-PolicyBrief1-Aug2022.pdf) on using new technology for illicit arms control following our joint presentation at United Nations in summer 2022

{{< include "/data/includes/disclaimer.html" >}}

## Introduction

During the early spring of 2022, VFRAME team partnered with Tech 4 Tracing on a field trip to an explosive ordnance training center in Europe. Using free-from-explosive (FFE) munitions, VFRAME carried out photogrammetry scans of submunitions including the 9N210 submunition (pictured above). Several hundred high-resolution photos were used to reconstruct a millimeter-accurate 3D model of the submunition's geometry. With the high-fidelity 3D model as a reference, thousands of procedurally randomized photorealistic synthetic training images were generated, annotated, then used to train an convolutional neural network object detection algorithm.

**The current 9N235/9N210 object detector model yields a 0.98 F1 score** on a custom benchmark dataset with challenging examples including partially occluded, partially exploded, damaged, dirt-covered munitions in various weather conditions from various camera angles and lenses. The new model (version 1C) was released on February 1, 2023, is available for download with a MIT license at [github.com/vframeio/vframe](https://github.com/vframeio/vframe), and improves the overall performance of the previous model (version 1B) released in July last year. 

{{% include "/data/9n235/metrics.md" %}}

The current version (1C) performs best on human-height videos or images created with smartphone camera that typically posted online to document scenes in conflict zones (i.e. OSINT sources) and is designed to handle typical artifacts common in online imagery including watermarks, compression, and light motion blur, and various image ratios. An additional version designed for aerial detection is planned for release later this year. 


### About VFRAME

VFRAME is a computer vision project that develops open-source technology for human rights research, investigative journalists, and conflict zone monitoring. After several years of research and development into synthetic data fabrication techniques using [3D-rendering](/3d-rendered-data) and [3D-printed](/3d-printed-data) data, this is the first publication of an object detection algorithm that uses all combined methods, as well as sufficient benchmark data to confirm the results. 

Many thanks to the [organizations](/funding) that have supported this project during the last several years and to VFRAME's latest partner [Tech 4 Tracing](/collaborations/#t4t) for facilitating access to the FFE munitions, as well as Fenix Insight for additional support and coordination on benchmark data development, SIDA/Meedan for continued operation support, and PrototypeFund for initial research support into synthetic data. 

## 9N235 Submunition

The 9N210 and 9N235 are high-explosive fragmentation submunitions, also known as cluster munitions. Upon detonation the explosive payload blasts metal fragments in all directions, indiscriminately killing or maiming  bystanders including non-combatant civilian. For this reason, cluster munitions are banned in 119 countries by the [Convention on Cluster Munitions](https://www.clusterconvention.org). Although neither Russian nor Ukraine are signatories (nor is the United States), they are still bound by international humanitarian law, which prohibits indiscriminate attacks.[^hrw_syria_cluster]

![3D visualization of finalized 9N235 photogrammetry model](images/vframe-9n235-material.jpg#watermark)

Recent documentation from Ukraine shows 9N235/9N210 submunitions have been widely deployed by Russia. Journalists and human rights researchers have documented dozens of instances where the cluster munitions were used in urban areas absent of military targets or personnel. In December 2022 HRW reported that"[s]ince the full-scale invasion of Ukraine, Russian forces have repeatedly used cluster munitions, which are inherently indiscriminate weapons, in attacks that have killed hundreds of civilians and damaged homes, hospitals, and schools."[^hrw_kherson] Other previous reports show it was used in attacks in Syria. Earlier, in March 2022, investigative group Bellingcat had already noted that the 9N235/9N210 cluster munitions were the "[most common type of cluster munition](https://twitter.com/bellingcat/status/1502237551146459137)" so far used in Ukraine.

Based on the early observation by Bellingcat, the unique visual appearance of the 9N235/9N210, and the continued high frequency of reports by other research organization, the 9N235/210 was selected as a preliminary candidate for object detection development. The next step was to analyze existing media reports and documentation to determine how well the object could be detected and whether it would be worth the development.

{{% include "/data/9n235/reports.md" %}}


## 9N235/9N210 Detectability

The 9N235 and 9N210 are nearly identical from their outside appearance. Each has the same 6 black fins, nosecone, body, dimensions, and approximately the same weight. The main difference is the internal configuration of the warhead. Otherwise, both use the same flawed fuze mechanism resulting in frequent unexploded ordnance (UXO). Even though the munitions contain a secondary self-destruction fuze with a 110 second delay, both have a high failure rate.[^gichd_ukraine_ed2] As a result, UXO often remain after an attack, posing a fatal threat to civilians. Below are examples of the submunition appears in recent documentation from Ukraine.

{{< three-col-images
    src1="images/osint/tw_9n235_FMr6VlmXIAI6iGN.jpg"
    src2="images/osint/tw_9n235_FM-_wlqaQAA0-1I.jpg"
    src3="images/osint/tw_9n235_FN0a5zIWQAMkN4S.jpg"
    caption1="Example documentation of 9N235/9N210 submunition on social media imagery. Source: https://twitter.com/olehbatkovych/status/1498285374153633797"
    caption2="Example documentation of 9N235/9N210 submunition on social media imagery. Source: https://twitter.com/Ukrain_War/status/1499628097208868869"
    caption3="Example documentation of 9N235/9N210 submunition on social media imagery. Source: https://twitter.com/eod205/status/1503387454258266118"
>}}

The combination of its high failure rate, frequent use, and distinctive appearance make the 9N235/9N210 a candidate for possible automated detection. The only way to test this hypothesis will be to build the object detector and evaluate its performance.

Though there is a problem. There is a limited number of photos with the 9N235/9N210 submunition online. At the time of starting this project it was only a few dozen. Now there are more. But it's still limited to a few hundred, of which many are near duplicates. After splitting that for train/test/val partitions it leaves nowhere enough data for training a robust object detector.

VFRAME is taking a new approach to building neural networks using art-driven, data-centric development. Instead of scraping biased images online or setting up sterile laboratory experiments, data is generated from the ground-truth up using an interdisciplinary combination of photography, photogrammetry, 3D-rendering, 3D-printing, custom software, and artistic forgery. This post outlines the steps taken to build a high-performance 9N235/9N210 detector with almost no data from online sources, except for use in the final benchmarking dataset to evaluate the algorithm's performance.

The first step will bypass the internet as a source of data and instead find access to the real submunition as the ground-truth source of data as a 3D model using photogrammetry.

<small><i class="fa fa-hammer" aria-hidden="true"></i> This post is a work in progress and is currently being revised for publication in a research report.</small>


## Photogrammetry

**Step 1**: Photogrammetry is the process of using multiple high-resolution photos to reconstruct an object's 3D geometry and surface texture. Creating 3D models of physical objects has become increasingly simple over the last decade, but there are many trade offs between different software, camera, and capture approaches. There are also dedicated 3D scanners that simplify the process further and high-end personal-computers/smartphones that integrate depth sensors with on-device photogrammetry processing. There is no single best approach. For this project, the goals were high-accuracy, portability, and the ability to use utilize existing hardware (DSLR camera and GPU workstation).

The most important step is not the technology but finding safe access to a free-from-explosive munition. The munition should also be undamaged otherwise the damaged areas will become part of the ground-truth geometry. It should also representative of the object as it appears in conflict, and not significantly altered during the free-from-explosive conversion.

To access the 9N235/9N210 submunition, VFRAME partnered with the NGO Tech 4 Tracing; an international, non-profit partnership working to apply new technologies to arms and ammunition control. In the early spring of 2022, both teams traveled to a weapons training facility in Europe and carried out the photogrammetry capture.

![Capturing the original 9N235/210 submunition using photogrammetry with an automated turntable and DSLR camera. Photo: &copy; Adam Harvey / VFRAME.io.](images/vframe_9n235_capture.jpg#watermark)

In total about 200 high-resolution photos were used to create the 3D model. An automated turntable was used to expedite the process. Each camera position in the graphic below shows the camera position for each photo.

![Photogrammetry scan of the 9N235 submunition by VFRAME in collaboration with Tech 4 Tracing. Graphic: &copy; Adam Harvey / VFRAME.io](images/vframe_t4t_9n235_photogrammetry.png#watermark)

After post-processing the captures and running the photogrammetry process (with some refinement), the final result is a millimeter-accurate 3D model. This becomes an ideal ground truth for generating synthetic training data.

![Rendering: &copy; Adam Harvey / VFRAME.io.](images/vframe-9n235-shading.jpg#watermark)



## Synthetic Data: 3D Rendered

**Step 2**: Synthetic data is an area VFRAME has focused heavily since 2019. It's a game-changing technology for computer vision and especially for detecting rare and dangerous objects, such as cluster munitions.

Typically, training images are gathered from online sources or from an existing imaging systems such as CCTV. Images are then manually annotated in-studio, or outsourced to annotation click-workers in foreign countries. This creates multiple issues, among them data security, data bias, labor exploitation, cost, and the possibility of errors.

Synthetic data solves many of these problems because the annotations are automatically generated by software, diversity and bias can be controlled for, weather conditions can be programmed, and it can lower the overall cost. To develop the 9N235/9N210 synthetic training dataset, over 10,000 images were rendered using various lighting environments, scene compositions, dirt variations, damage variations, and camera lenses. Each factor can be deliberately controlled for.

The way the object appears in the synthetic image is based on observations from the preliminary research. It reflects how the submunition lands, how the material will weathering, and the terrain where its being documented. Often the submunition is lodged into a soft ground surface with all 6 black tail fins pointing upright. But sometimes the tail fins will break leaving a metal tube with anywhere from 0-6 fins. This can also be modeled for and is important to control the confidence levels for false positives.

The example rendering below uses a 40mm lens, F5.6 aperture, afternoon lighting, centered on the 9N235 with all 6 fins intact. To improve diversity every image is procedurally randomized then manually reviewed to ensure the training data aligns with the expected outcomes.


![3D-rendered image with a 9N235 submunition used in the training dataset. Image &copy; Adam Harvey / VFRAME 2023](images/vframe_9n235_synthetic_image.jpg#watermark)

![Color-coded pixel mask used to automatically generate annotation data. Image &copy; Adam Harvey / VFRAME 2023](images/vframe_9n235_synthetic_colored.png#watermark)

![Auto-generated mask and bounding box values for training data. Image &copy; Adam Harvey / VFRAME 2023](images/vframe_9n235_synthetic_bbox.jpg#watermark)


## Synthetic Data: 3D Printed

**Step 3**: With enough work, 3D-rendering can achieve convincing photorealism but it still contains artifacts of a simulated world and risks overfitting if the target objects are too rigid or lack diversity. Based on research carried out over the last several years, algorithms trained on synthetic data will always overfit and produce overconfident and misleading results if 3D-rendered synthetic images are used in the test dataset. To escape this curse of simulation, VFRAME has pioneered a hybrid approach that uses [3D-printed data](/docs/research/3d-printed-data) to generate synthetic images in the "real-world".


![3D printing multi-part 9N235 submunition replica for use in simulated benchmark photos and videos](images/vframe-9n235-replica-3d-printed.jpg#watermark)

3D-printed data refers to the process of creating a 1:1 physical replica of an object using 3D-scanning, 3D-printing, and artistic forgery. By recreating the digital surrogate object in the real world it escapes the limitations of 3D-rendered worlds and bridges the gap towards a more real reality. In other words, the 3D printed replica can now be placed in any staged scene or environment and contribute higher-fidelity data. 

Another significant advantage of using 3D-printed data for submunitions is safety. Obtaining submunitions always involves risk, and removing the explosives material to make it FFE involves further risk for EOD personnel. The 3D-printed replicas are inert, hollow, plastic, and can even made using environmentally responsible bioplastics like PLA.

The results are not perfect but can be convincingly real. Below are two photos of a 9N235/9N210 submunitions. One is real and one is fake. Both are covered in mud and photographed with the same camera in wet forest terrain. 

{{< two-col-images
    src1="images/9n235_t4t_iphone_02_0140.jpg"
    src2="images/vframe-9n235-replica-01.jpg"
    caption1="One is real and one is fake. Two photos of 9N235 submunitions used for benchmark data to evaluate detection performance when covered in mud."
    caption2="One is real and one is fake. Two photos of 9N235 submunitions used to evaluate detection performance when covered in mud."
>}}

## Benchmark Data

With the submunition 3D-modeled, synthetic images 3D-rendered, and 3D-printed models photographed, the next step is to curate the benchmark dataset to how well, or not, the neural network is able to detect the object.

Benchmark data is essential for understanding the accuracy of the trained object detector. An easy benchmark dataset yields unrealistic expectations for what the detector is capable of. To overcome bias in  benchmark data, it's helpful to spread this task across many seasons, terrain, contributors, and hardware. Images should contain easy, medium, difficult scenarios. Not only is diversity useful for the model metrics, but it helps communicate to end users how well the detector can be expected to perform when, for example, a munition is partially exploded or broken. Or when it will trigger false-positives on similar looking objects. This is especially important for objects that pose a risk to life.

The results also administrators fine-tune the threshold parameter for greedy or conservative deployments. Because the output is always a probabilistic determination the actual deployment thresholds must be customized to the target environment. For example, a million-scale OSINT application could first triage everything above 90% accuracy, then look deeper at lower confidence matches when time permits. Or a aerial survey of an attack site could use a low-threshold to detect anything with a close-match, which would do a better job detecting partially exploded and partially hidden munitions.


![64 images from the 9N235 benchmark dataset created using the 3D printed replica](images/vframe_9n235_benchmark_montage.jpg#watermark)

## Model Metrics

The model is trained using synthetic data but evaluated using multiple types of real data, including images sourced online. The most common metrics are applied to measure how well it can detect the true-positives (recall), how well it ignores the false-positives (accuracy), and how precise the bounding boxes are (mAP). These metrics are combined into one score called the F1 to give an summarized performance metric.

For this model the F1 score is 0.98 at 0.641 confidence. This means that if you set the confidence threshold in the processing software you should expect high-accuracy results, with only a few images missed. If you want to detect everything (recall=1.0) the confidence could be dropped to 0.0, but this would trigger more false positives and bring the accuracy down to 0.2 which might be acceptable in certain scenarios.

{{< two-col-images
    src1="images/training/F1_curve.png"
    src2="images/training/P_curve.png"
    caption1="9N235 L6 x 1280px F1 curve"
    caption2="9N235 L6 x 1280px precision curve"
>}}

{{< two-col-images
    src1="images/training/R_curve.png"
    src2="images/training/PR_curve.png"
    caption1="9N235 L6 x 1280px recall curve"
    caption2="9N235 L6 x 1280px precision-recall curve"
>}}

Another way to visulize performance is to look at the confusion matrix, which shows the true positive detections (2076) compared to the false positive (23) and false negative (63). The numbers here are highly dependent on the quality of the benchmark test images.


![9N235 L6 x 1280px confusion matrix](images/training/confusion_matrix.png)


## Test Images

**Step 6**: Finally, the following images show examples from the test set. Use these as a reference to understand the confusion matrix. Consider that when the object is partially occluded by tall grass it can still be detected as along as most of the black fins are visible. Also, the test images are vertical, but most of the synthetic training images were horizontal. It's important to test all aspect ratios.


{{< two-col-images
    src1="images/detections/9n235_ah_scene_01_000010.jpg"
    src2="images/detections/9n235_ah_scene_01_000129.jpg"
    caption1=""
    caption2=""
>}}


When there's motion blur, the detector should still work well. Here an older camera was used with a poor quality sensor that also produces overexposed areas on the metal. The detector still works fine is able to ignore the false-positive decoys placed in the scene.

![](images/detections/9n235_vf_02_cam_h_000207.jpg#watermark)

Another test shows if the detector is smart enough to differentiate between a complex scene of metal tubes and submunitions mixed together. Most are detected with over 90% accuracy, but the object in the top middle drops to 75% because the black fins are less prominent here and wet leaves are covering an important detail where the cylinder meets the fin assembly.

![Benchmark image created in collaboration in Fenix Insight](images/detections/9n235_vf_02_cam_h_000052.jpg#watermark)

Referring back to the 3 images used as reference to evaluate the detectability, these are now uses as benchmark data to evaluate the detector's performance. None of these images were included in the training dataset. The results speak to the power of an artist-driven, data-centric approach to developing neural networks. All 3 objects were easily detected, even the submunition partially visible and still inside the rocket.

{{< three-col-images
    src1="images/osint_detections/tw_9n235_FMr6VlmXIAI6iGN.jpg"
    src2="images/osint_detections/tw_9n235_FM-_wlqaQAA0-1I.jpg"
    src3="images/osint_detections/tw_9n235_FN0a5zIWQAMkN4S.jpg"
    caption1="Detection result on social media reference imagery. Source: https://twitter.com/olehbatkovych/status/1498285374153633797"
    caption2="Detection result on social media reference imagery. Source: https://twitter.com/Ukrain_War/status/1499628097208868869"
    caption3="Detection result on social media reference imagery. Source: https://twitter.com/eod205/status/1503387454258266118"
>}}

## Performance

The model is trained in multiple architectures for deployment on workstations or mobile/edge devices. Running on a HEDT (high-end desktop workstation) achieves a maximum 187 FPS with the nano architecture and . Referring to the model metric table, the full performance (recommended) model reaches 43 FPS. 

![Frames per second on NVIDIA 3090 at 1280 pixels inference size averaged over 100 iterations for nano, small, medium, and large YOLOV5 architectures at batch size 8 using .pt model format](images/9n235-fps-bs8.png)

{{% include "/data/9n235/metrics.md" %}}

### Future Reports

- OSINT analysis for 100K size image dataset (April 2023)
- OSINT analysis for million-scale video dataset (May 2023)

### Credits

- Adam Harvey: AI/ML systems, synthetic data, object detection, 3D printing
- Josh Evans: photogrammetry, 3D model design
- Tech 4 Tracing: EOD coordination
- Fenix Insight: additional replica/surrogate fabrication and benchmark dataset collaboration

### License

- The model files are released open-source with an MIT license. They are free to use for commercial systems **only** if the license is included and distributed with any software deployments.
- Unless otherwise noted, all images are &copy; Adam Harvey / VFRAME.io

### Funding

- Initial development self-supported by workshops and exhibition fees (2022-2023)
- Advancements and performance improvements supported by [Fenix Insight](https://fenix-insight.online/) (2023)
- Development of the 9N235/9N210 detector is largely based on several years of research supported by grants from Prototype Fund and SIDA/Meedan (2019-2021)
- Read more about VFRAME's supporters [here](/funding)

---

{{< include "/data/includes/disclaimer.html" >}}


[^hrw_ukraine_cluster]: https://www.hrw.org/news/2022/05/11/end-cluster-munition-attacks-ukraine
[^hrw_syria_cluster]: https://www.hrw.org/news/2016/07/28/russia/syria-widespread-new-cluster-munition-use
[^hrw_kherson]: https://www.hrw.org/news/2022/12/13/ukraine-apparent-cluster-munitions-hit-kherson
[^gichd_ukraine_ed2]: Explosive Ordnance Guide for Ukraine https://www.gichd.org/en/resources/publications/detail/publication/explosive-ordnance-guide-for-ukraine-second-edition/