# Cut.js

Cut.js (name inspired from "cutout animation") is a minimal JavaScript library for composing high-performance, dynamic and interactable HTML5 visual interfaces from images textures. It works with modern browsers and mobile devices and intended to be used for game and visual app development.

[API Doc](api-doc.js)

### How it works

A cut.js app consists of image textures, cutout (sprite) definitions and a tree structure. Each node in tree includes image cutouts and/or child nodes. Each node is pinned (transformed) against its parent and pastes its cutouts on rendering.

Each rendering cycle consists of ticking and painting the tree. Ticking is used to update the tree nodes and then on painting each node transforms according to its pinning and pastes its cutouts and then delegates to its children.

Rendering is retained and pauses in each cycle unless/until it is touched directly or indirectly by updating it.

### Example

Following code demonstrate a simple use case. Cut.Loader and Cut.Mouse are pluggable components.

```js
  Cut.Loader.load(function(root, container) {

    Cut.Mouse.subscribe(root, container);

    // scale and resize to cover container
    var viewport = Cut.create().appendTo(root).pin({
          width : 500,
          height : 300
      }).listen("resize", function(width, height) {
        this.pin({
          resizeMode : "in",
          resizeWidth : width,
          resizeHeight : height
        });
      };

    var colors = [ "green", "blue", "purple", "red", "orange", "yellow" ];
  
    var row = Cut.row(0.5).appendTo(viewport).pin("align", 0.5).spacing(1);
    for (var i = 0; i < colors.length; i++) {
      Cut.image("color:" + colors[i]).appendTo(row)
        .listen(Cut.Mouse.MOVE, function(ev, point) {
          this.tween().clear().pin({
            scaleX : Cut.Math.random(0.8, 1.6),
            scaleY : Cut.Math.random(0.8, 1.6)
          });
          return true;
        });
    }

  });

  Cut.addTexture({
    name : "color",
    imagePath : "colors.png",
    cutouts : [
      { name : "red",    x : 30, y : 0,  width : 30, height : 30 },
      { name : "purple", x : 30, y : 30, width : 30, height : 30 },
      { name : "blue",   x : 60, y : 0,  width : 30, height : 30 },
      { name : "orange", x : 60, y : 30, width : 30, height : 30 },
      { name : "yellow", x : 90, y : 0,  width : 30, height : 30 },
      { name : "green",  x : 90, y : 30, width : 30, height : 30 }
    ]
  });
```

### Examples

[![Row, Dynamic](https://raw.github.com/piqnt/cut.js/master/examples/row-dynamic/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/row-dynamic/index.html)
[![Row, Static](https://raw.github.com/piqnt/cut.js/master/examples/row-static/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/row-static/index.html)
[![Column x Row](https://raw.github.com/piqnt/cut.js/master/examples/grid/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/grid/index.html)
[![Number](https://raw.github.com/piqnt/cut.js/master/examples/number/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/number/index.html)
[![Tile](https://raw.github.com/piqnt/cut.js/master/examples/tile/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/tile/index.html)
[![Stretch](https://raw.github.com/piqnt/cut.js/master/examples/stretch/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/stretch/index.html)
[![Bars](https://raw.github.com/piqnt/cut.js/master/examples/bars/thumbnail.png)](https://rawgithub.com/piqnt/cut.js/master/examples/bars/index.html)


### Projects

[O!](http://piqnt.com/o/) (Open-source), [006](http://piqnt.com/006/), [Four](http://piqnt.com/4/four/)


### License

Copyright (c) 2013-2014 Ali Shakiba, Piqnt LLC and other contributors  
Available under the MIT license