# Leaflet RouteBoxer

This is a Leaflet implementation of the [RouteBoxer](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/routeboxer/docs/examples.html) Class from Google.

The RouteBoxer class generates a set of L.LatLngBounds objects that are guaranteed
to cover every point within a specified distance of a path, such as that generated
for a route by an OSRM directions service.

## Example

Check out the example [demo](http://stephangeorg.github.io/leaflet-routeboxer/example/)

## Install

```
bower install leaflet-routeboxer
```

## Usage

You need to pass an array of L.Latlng objects (route) to the L.RouteBoxer.


```javascript

var route = [
  [50.5, 30.5],
  [50.4, 30.6],
  [50.3, 30.7]
];
var boxes = L.RouteBoxer.box(route, distance);

```

### Using w/ OSRM service

OSRM uses polyline encoding to save bandwith. To decode the polyline you can use
[Leaflet.encoded](https://github.com/jieter/Leaflet.encoded).

```javascript

// data.route_geometry is the result from a OSRM endpoint
var route = new L.Polyline(L.PolylineUtil.decode(data.route[0].geometry));
var boxes = L.RouteBoxer.box(route, distance);

```
