---
description: Describe contribution and library.
---

# Contribution and customization

## Contribution

In case you haven't noticed yet, I'm a pretty big fan of the [Elm programming language](http://elm-lang.org/). It provides a strong safety thanks to its type system, by forcing you to consider all cases that could happen. As a consequence, a program that compiles will **most likely never produce a runtime error**. The only bugs that can happen, are those related to the app behavior, or browser compatibility. Thus, contrary to most alternatives, this application should **perform extremely reliably**. If you find any bug, please report it by creating an issue in the [github project page](https://github.com/mpizenberg/annotation-app/issues).

Whether you have an idea to improve the application, a question, feedback on a use case, a bug to report, implement a feature, ... **the best way to start contribution is communication**. You can find me on the [Elm slack](http://elmlang.herokuapp.com/) \(@mattpiz\) or simply create an issue on github. Before creating an issue, please search for an already existing similar one.

Currently issues are labelled with one or more of the following labels:

* "**bug**": Something isn't working
* "**feature request**": Request a new feature
* "**question**": Further information is asked
* "**UI**": User Interface
* "**good first issue**": Good for newcomers
* "**help wanted**": Extra attention is needed
* "**meta**": meta

Some simple features are purposely left undone and labelled "[**good first issue**](https://github.com/mpizenberg/annotation-app/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)" to enable potential contributors to dive into the application code in a gentle way. This is for example the case of:

* [Keyboard shortcuts](https://github.com/mpizenberg/annotation-app/issues/3)
* [Allow zooming with wheel](https://github.com/mpizenberg/annotation-app/issues/6)
* [Using a different mouse cursor for each tool](https://github.com/mpizenberg/annotation-app/issues/18)
* [Adding tooltips on buttons](https://github.com/mpizenberg/annotation-app/issues/21)

## Advanced customization

Customizations can be organized at four levels:

1. **Configuration**: by changing the configuration Json file, you can change the tools provided.
2. **Interop JavaScript API**: the Elm application have interop with JavaScript defined in ports, as described in the "Application code structure" page. One way of augmenting the interactions possibilities with the application could be to design ports in such a way that key messages are exposed as an API.
3. **Full interface rewrite**: the application code structure is described in the corresponding page. In case one needs a feature too different from the shape and goals of this application, one can simply fork the open source application code, and change the interface code.
4. **Image annotation library contribution**: some changes might require completely new functionalities, like implementing another annotation tool. The foundation of this application is the Elm package [`mpizenberg/elm-image-annotation`](https://github.com/mpizenberg/elm-image-annotation). Such changes would happen here.

### The elm-image-annotation package

The foundation of this application is the Elm package [`mpizenberg/elm-image-annotation`](https://github.com/mpizenberg/elm-image-annotation). It is designed as an API to create, modify and visualize geometric shapes useful in the context of image annotation.

The primary geometric data structures are each defined in a separate module, under the `Annotation.Geometry` namespace. If you want to introduce a new geometric prior for annotations, this is the place where to create a new module.

* `Annotation.Geometry.BoundingBox`: provides functions to create, modify and serialize \(Json\) bounding boxes.
* `Annotation.Geometry.Contour`: provides functions to create, modify and serialize \(Json\) countours, rather called polygons in this application.
* `Annotation.Geometry.Outline`: provides functions to create, modify and serialize \(Json\) outlines.
* `Annotation.Geometry.Point`: provides functions to create, modify and serialize \(Json\) points.
* `Annotation.Geometry.Stroke`: provides functions to create, modify and serialize \(Json\) strokes \(lines\).

The package also have the following modules, defined in the `Annotation` namespace:

* `Annotation.Color`: exposes a `toString` function converting a Color into string usable in DOM elements like `"rgba(255,0,0,1)"`. It also exposes a color palette color-blind and print friendly.
* `Annotation.Style`: defines types describing appearance of points, lines and fillings.
* `Annotation.Svg`: exposes functions rendering Svg elements from geometric objects and appearance styles.
* `Annotation.Viewer`: this is the module managing the visualization area, with zooming, and movements, relative to an image frame.

If you are interested in creating another rendering target than SVG, like canvas, webgl, ..., it would require the creation of alternative modules to `Annotation.Svg` and `Annotation.Viewer`.

