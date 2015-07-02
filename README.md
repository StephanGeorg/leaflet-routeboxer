# Leaflet RouteBoxer

This is a Leaflet implementation of the [RouteBoxer](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/routeboxer/docs/examples.html) Class from Google.

The RouteBoxer class generates a set of L.LatLngBounds objects that are guaranteed
to cover every point within a specified distance of a path, such as that generated
for a route by an OSRM directions service.

## Demo

Check out the example: [Demo](http://stephangeorg.github.io/leaflet-routeboxer/example/)

## Usage

```javascript

/**
 * Callback function to draw polyline and calculate bounds
 *
 */
function drawRoute(data){

  var route = new L.Polyline(L.PolylineUtil.decode(data.route_geometry, 6)); // OSRM polyline decoding
  var distance = 10 // distance in km from route

  route = route.getLatLngs();

  var boxes = L.RouteBoxer.box(route, distance);
  var boxpolys = new Array(boxes.length);

  for (var i = 0; i < boxes.length; i++) {
    L.rectangle(boxes[i], {color: "#ff7800", weight: 1}).addTo(this.map); // draw rectangles based on Bounds
  }
  var polyline = L.polyline(route).addTo(this.map); // draw original route
}


// Waypoints for the route
var loc = [
  '53.553406,9.992196',
  '48.139126,11.580186'
];

// Use Mapzen only for testing
var url = 'http://osrm.mapzen.com/car/viaroute?';

// Add all waypoints
for(var i=0; i<loc.length;i++) {
  url = url + '&loc=' + loc[i];
}

// Get route from Mapzen
var jqxhr = $.ajax({
  url: url,
  data: {
    instructions: false,
    alt: false
  },
  dataType: 'json'
})
.done(function(data) {
  drawRoute(data);
});

```
