# Backbone-browserify
## packaged for use with [node-browserify](https://github.com/substack/node-browserify).

```bash
npm install backbone-browserify
```

**Important:** You must require `jquery-browserify` or Zepto (untested) with Browserify before you require Backbone, just like normal.

Just add it to your browserify require list and use it! Make sure you also have Underscore installed via npm as Backbone will automatically require it.

### Server Side
````javascript
browserify({
  require : [ 'jquery-browserify', 'backbone-browserify' ]
});
````

... or to alias it to just "backbone":

````javascript
browserify({
  require : { jQuery: 'jquery-browserify', backbone: 'backbone-browserify' }
});
````

#### Express example
```js
app.configure(function(){
  app.set('views', __dirname + '/views');
  app.set('view engine', 'jade');
  app.use(express.bodyParser());
  app.use(express.methodOverride());
  app.use(app.router);
  app.use(express.static(__dirname + '/public'));
  app.use(browserify({
    require : { jQuery: 'jquery-browserify', backbone: 'backbone-browserify' }
  }));
});
```

### Client Side
````javascript
var $ = jQuery = require('jquery-browserify'),
    Backbone = require('backbone-browserify'),
    MyView = Backbone.View.extend({
        el: 'body',
        initialize: function() {
            this.render();
        },
        render: function() {
            $(this.el).html('<h1>Oh hi</h1>');
        }
    });
    
$(document).ready(function() { var myView = new MyView(); });
````

... or if you aliased it to 'backbone':

````javascript
var $ = jQuery = require('jquery'),
    Backbone = require('backbone'),
    MyView = Backbone.View.extend({
        el: 'body',
        initialize: function() {
            this.render();
        },
        render: function() {
            $(this.el).html('<h1>Oh hi</h1>');
        }
    });
    
$(document).ready(function() { var myView = new MyView(); });
````