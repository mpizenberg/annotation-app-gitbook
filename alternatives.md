---
description: Similar available image annotation applications.
---

# Alternatives

You may find on wikipedia a [list of manual image annotation tools](https://en.wikipedia.org/wiki/List_of_manual_image_annotation_tools). Not all are equal in functionality or accessibility but some of them are pretty good. Also noticeable, few have been here for ages like LabelMe, bust most are less than 1 or 2 years old. This regain in popularity is obviously correlated with machine learning popularity, especially **neural networks**, and its requirements for massive annotated training datasets.

We've curated a bit the wikipedia list to keep only Web applications, providing at least bounding boxes and polygonal annotations, with a simple interface. Please let us know if you feel we've forgotten yours. To this date \(April 2018\), the most interesting options, according to us are the following \(most interesting features in bold\).

| Application | Year | Features | Type | License |
| --- | --- | --- | --- | --- |
| [LabelMe](http://labelme.csail.mit.edu/Release3.0/) | 2008 | bbox, polygon, iterative segmentation -- **Amazon Mechanical Turk integration** | Server | **OSS** |
| [VGG Image Annotator \(VIA\)](http://www.robots.ox.ac.uk/~vgg/software/via/) | 2016 | bbox, polygon, circle, ellipse, point -- **region attributes** | Client | **OSS** |
| [Labelbox](https://www.labelbox.io/) | 2018 | bbox, polygon, point -- **configurable interface** -- **collaborative annotations tasks management -- export to COCO, Pascal VOC formats** | Server | Private, OSS Fronted only |
| [Dataturks](https://dataturks.com/) | 2018 | bbox or polygon -- **annotations tasks management** | Server | Private |

Amazon Mechanical Turk integration is on the roadmap to enable crowd-sourced annotation tasks. Just like VIA, our application is purely client side, meaning that no data is uploaded to the server. Images are loaded from files and annotated locally, in the browser. Region attributes, as featured in VIA are a very interesting feature. A similar feature that we are thinking of but is not implemented is annotation comment.  Export to standard formats as Microsoft COCO or Pascal VOC are not implemented. Just like Labelbox is doing, there could be a simple conversion script from our format to each of these. Let us know if you did one. One thing we are not going to do, at least for the near future, is a collaborative tasks management server. We believe that our tool is flexible enough that you could integrate it in such server if you need it.

