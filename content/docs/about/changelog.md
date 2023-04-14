---
title: Changelog
description: Development updates and changes
bookToc: false
url: /changelog
date: 2023-03-16
modified: 2023-03-28
images:
- https://vframe.io/3d-rendered-data/images/ao25_wireframe.jpg
---


# Development Updates

Short updates on VFRAME development progress, bug fixes, model releases, and news to provide more transparency into project development and activity.

April 14
- Retrain the 9N235/9N210 detectors with new data to better handled damaged and partial objects, and reduce false positives
- Update 9N235 detector models to version 1D <https://demos.vframe.io>
- Separate SHA256 media deduplication script to separate command group `dedup` and small usability improvements for handling added and removed media items

April 13
- Moved modelzoo.vframe.io --> <https://demos.vframe.io> 
- Updated the 9N235/9N210 nano and small architectures with version 1D. This update reduces false positives and improves recall on heavily damaged 9N210/9N235 submunitions based on reference photos from Ukraine.

March 30
- Submit research report to James Madison University journal on building the 9N235 detector and applicability of this technology to mine clearance and EOD work

March 27
- Remove verbose from `media-attrs-plot`, add `media-attrs-summarize` for simpler summaries

March 16
- Updated `media-attrs` with more manual binning interval and size options. The auto-binning yielded arbitrary intervals.
- Updated site to add work in progress for the Uragan, RBK-250, and RBK-500
- Improved clarity on 9N235 detector page
- Twint (for scraping Twitter) now seems to be fully broken

March 2
- Moved `media-attrs` out of development into public code. See research post on plotting [media attributes](/media-attributes)
- Updated website, adding search and model development previews for current research
- Begin changelog for more project development transparency

February
- Released updated 9N235 detection models in n/s/m/l model architectures for YOLOV5 framework in .pt and .onnx formats
