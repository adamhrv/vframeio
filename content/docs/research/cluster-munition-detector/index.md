---
Title: Cluster Munition Detector
display_order: 3
published: 2019-03-01
Summary: Training object detection algorithms to locate illegal munitions
bookToc: False
bookHidden: true
bookDraft: True
draft: True
bookSearch: False
sitemap_exclude: True
---

{% include "research_title.html" %}

![Caption: Detecting AO2.5RT cluster munitions is challenging due to the variety of appearances and fractured assemblies.<br>Without a large enough training dataset, the detector fails to find all munitions.](bd7cbdbee258a9a22a0e4244243a2075e27e694613a5c0abe5aeb8ace29c0751_960.jpg)

Since VFRAME started in 2017, building a cluster munition detector has always been the priority, but attaining high accuracy has been more difficult than expected. Munitions can appear in many different ways. For example, the AO-2.5RT cluster munition can appear fully intact, split in half with and without arming fins, or the arming fins may appear alone. Each of these variations might be found upside down, covered in dirt, damaged, or partially occluded. Detecting a *AO-2.5RT cluster munition* actually means detecting all of these visual appearances.

The hierarchy below shows how each munition is sub-classed into different visual states, each of which are annotated separately for training and then combined during inference using a hierarchical object detection model.

![Caption: Hierarchy of cluster munition annotations](vcat_hierarchy.png)

Using this approach for labeling, several hundred annotations are manually created for each object in each class. Then, the Darknet/YoloV3 training network is used to create object detection models. 


## Cluster Munition Detector Prototypes

Prototype #1 (below) initially worked well for cluster munitions that appeared close the camera, but it missed objects that were smaller or covered in dirt. Prototype #3 was trained using more examples and small imagery and has higher detection accuracy on smaller objects. However, the overall accuracy is still quite low likely due to insufficient training data.

To mitigate these issues, we have produced new models trained on [synthetic datasets](/research/synthetic-datasets/).



### Acknowledgments

<small>This research has been supported by funding from PrototypeFund (DE).</small>
