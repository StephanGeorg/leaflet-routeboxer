# Leaflet RouteBoxer

This is a Leaflet implementation of the [RouteBoxer](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/routeboxer/docs/examples.html) Class from Google.

The RouteBoxer class generates a set of L.LatLngBounds objects that are guaranteed
to cover every point within a specified distance of a path, such as that generated
for a route by an OSRM directions service.

## Demo

Check out the example: [Demo](http://stephangeorg.github.io/leaflet-routeboxer/example/)

## Usage

```javascript

// Waypoints for getting a route of
var loc = [
  '53.553406,9.992196',
  '48.139126,11.580186'
];

var url = 'http://osrm.mapzen.com/car/viaroute?';
var _this = this;

for(var i=0; i<loc.length;i++) {
  url = url + '&loc=' + loc[i];
}

var jqxhr = $.ajax({
  url: url,
  data: {
    instructions: false,
    compression: false,  // compression must be switched of
    alt: false
  },
  dataType: 'json'
})
.done(function(data) {
  var distance = 10 // distance in km from route
  var boxes = L.RouteBoxer.box(route, distance);
  var boxpolys = new Array(boxes.length);

  for (var i = 0; i < boxes.length; i++) {
    L.rectangle(boxes[i], {color: "#ff7800", weight: 1}).addTo(this.map); // draw rectangles based on Bounds
  }
  var polyline = L.polyline(route).addTo(this.map); // draw original route
})
.fail(function(data) {
  console.log(data);
});

```
