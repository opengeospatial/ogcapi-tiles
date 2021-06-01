# Quickstart Guide to implementing [OGC API - Tiles](https://github.com/opengeospatial/OGC-API-Tiles)

## About

This guide is intended to communicate the key pieces of the Tiles API standard so that implementors can get started 
without having to dig through the longer specification.

## Introduction

OGC API - Tiles provides a standard way to describe web map tile sets for clients to consume. It is the successor to 
[WMTS](https://en.wikipedia.org/wiki/Web_Map_Tile_Service), updated to use JSON, in line with the spatial data on the web 
best practices. It also is designed to be a 'building block', that can plug into the OGC API suite, but can also be used
as a standalone piece. It is similar to [TileJSON](https://github.com/mapbox/tilejson-spec), adding the ability to 
handle alternate projections and fitting into the OGC API suite of standards.


## TileSet Link

Any resource that is represented in JSON can provide a link to a ‘tileset’ JSON object that provides the necessary 
metadata to enable a client application to formulate a tile request. This could be an OGC Collection, OGC Item (from OGC API - 
Features), or a custom resource (even an ‘ephemeral’ resource like a search response). But the resource must have a links 
array that includes an object with a rel  of ‘tiles’ and a type of ‘application/json’, and the `href` must return the Tiles 
Description object specified below.    

```
  "links": [
    ...
    {
      "href": "http://data.example.com/collections/buildings/tiles",
      "rel": "http://www.opengis.net/def/rel/ogc/1.0/tileset"
      "type": "application/json",
    }
  ]
}
```

This communicates to any client that the link contains the JSON metadata to access the tiles of this particular resource. 

## TileSet response

The response of this link type is the JSON object that contains the information to enable a client application to formulate a 
tile request that represents the resources that created the link. The current minimum response in the specification is:

```
{
  ...
  "tileMatrixSetURI": "http://www.opengis.net/def/tilematrixset/OGC/1.0/WorldMercatorWGS84Quad",
  "dataType": "map",
  "links": [
    ...
    {
     "href": "http://data.example.com/collections/buildings/tiles/WorldMercatorWGS84Quad",
     "rel": "self",
     "type": "application/json",
    },
    {
     "href": "http://data.example.com/collections/buildings/tiles/WorldMercatorWGS84Quad/{tileMatrix}/{tileRow}/{tileCol}.png",
     "templated": true,
     "rel": "item",
     "type": "image/png",
    }
   ...
  ]
}
```

This JSON object is called the TileSet Metadata, and its full set of options are specified in the [TileSetMetadata conformance 
class](https://github.com/opengeospatial/2D-Tile-Matrix-Set/blob/master/standard/clause_8_tileset_metadata.adoc#tilesetmetadata-requirements-class) of
the [2D Tile Matrix Set](https://github.com/opengeospatial/2D-Tile-Matrix-Set) standard.

The `tileMatrixSetURI` can go to one of 8(?) preset OGC tilematrices (TODO: Add links / info here), or it can define a custom tileMatrixSet. Most tile
services are in Web Mercator, so if you don't know what projection your tile service is in then use the `WorldMercatorWGS84Quad` and it will likely be
right.

The `dataType` can be one of three options - `map`, `vector` and `coverage`. This refers to (TODO: get guidance on what these 
things mean and when implementers should actually use them). 

And then the templated link provides the key URL template to the actual tiles. You should provide one full link for each `type` of tile response
you support.

TODO: Figure out what to do if your tile server represents vector data as both .png and vector tiles, are those different `dataType` options, or just different media types. Add clarification.

TODO: Figure out how this response works if you have multiple projections of your tile set, and add that.

The specification provides advanced options in the `tileMatrixSetLinks` to specify your own projections and matrices. For
now just use the exact example above if your data is in WebMercator XYZ (as most web tiles are).

TODO: Add info on how to make the template match your server. And clarify if people have to include the tileMatrixSetID if 
they just have one

### Fuller Response

While the minimal response above is sufficient to get started, there are a number of useful fields that you can include. The following example
is a good example for the type of information to ideally include.

{
  ...
  "title": "Buildings of San Francisco",
  "boundingBox": {
    "lowerCorner": [50,50],
    "upperCorner": [100,100]
  }
  "tileMatrixSetURI": "http://www.opengis.net/def/tilematrixset/OGC/1.0/WorldMercatorWGS84Quad",
  "dataType": "map",
  "links": [
    ...
    {
     "href": "http://data.example.com/collections/buildings/tiles/WorldMercatorWGS84Quad",
     "rel": "self",
     "type": "application/json",
    },
    {
     "href": "http://data.example.com/collections/buildings/tiles/WorldMercatorWGS84Quad/{tileMatrix}/{tileRow}/{tileCol}.png",
     "templated": true,
     "rel": "item",
     "type": "image/png",
    }
   ...
  ],
  "tileMatrixSetLimits":
  [
    { "tileMatrix" : "0", "minTileRow" : 0, "maxTileRow" : 0, "minTileCol" : 0, "maxTileCol" : 0 },
    { "tileMatrix" : "1", "minTileRow" : 0, "maxTileRow" : 0, "minTileCol" : 1, "maxTileCol" : 1 },
    { "tileMatrix" : "2", "minTileRow" : 1, "maxTileRow" : 1, "minTileCol" : 2, "maxTileCol" : 2 },
    { "tileMatrix" : "3", "minTileRow" : 3, "maxTileRow" : 3, "minTileCol" : 4, "maxTileCol" : 4 },
    ...
  ]
}

TODO: I have no idea if the boundingBox is correct here, I'm not great at reading UML and couldn't find the description of the structure
or an example - the link didn't work. Also not sure why it doesn't use the same bounds construct as OGC API Collections.

TODO: Explain the fields

TODO: Add more options that 'most' people would be interested in.

## Examples

TODO: Include links to a number of complete examples, as often the '...' can leave people unsure as to what actually goes there. 

