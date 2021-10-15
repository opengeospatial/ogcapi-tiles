# Quickstart Guide for Clients

For Coverage Tiles, see also the _OGC API - Coverages_ [coverage tiles conformance class](https://docs.opengeospatial.org/DRAFTS/19-087.html#rc-coverage-tiles-section).

For Map Tiles, see also the _OGC API - Maps_ [map tiles conformance class](https://docs.ogc.org/DRAFTS/20-058.html#_relationship_to_ogc_api_tiles).

## How to retrieve map tiles, coverage tiles, or vector tiles
_from an OGC API landing page or collection of geospatial data step by step_

### Follow the links approach
***NOTE: This approach is recommended for generic clients to ensure maximum interoperability.***

***NOTE: The link relation types shown here are abbreviated and should be prefixed by `http://www.opengis.net/def/rel/ogc/1.0/` unless they are registered with [IANA](https://www.iana.org/assignments/link-relations/link-relations.xhtml).***

* Visit the landing page (***start here if you have a link to an OGC API landing page***)
  - discover a link to collections (rel: `data`) or to a list of tilesets (rel: `tilesets-map` for map tiles, `tilesets-vector` for vector tiles, `tilesets-coverage` for coverage tiles)
* Visit the /collections page (if wishing to access tiles from a specific collection)
  - look for a collection of interest in the `collections` array and select one
  - look for a link with rel: `self` in that collection for a link to the collection
* Visit the selected collection link (if requesting tiles for a specific collection, ***start here if you already have a link to a collection***)
  - look for the `links` property and select a link of the relation type for the desired type of tiles (e.g. rel=`tilesets-map`, `tilesets-vector` or `tilesets-coverage`)
* Visit that link to the list of tilesets
  - look for a tileset in the `tilesets` array using a supported TileMatrixSet, based on the `tileMatrixSetURI` (for registered TileMatrixSets) and/or a link to a TileMatrixSet definition (rel: `tiling-scheme`)
  - look for the `links` property and select the link for the tileset itself (rel: `self`)
* Visit the link to the tileset (***start here if you already have a link to a tileset***)
  - look for the `links` property and select a `link` with rel=`item` (templated) and `type` with the format you like to obtain the tile URL template.
  - if no `type` is provided, multiple formats may be supported: use HTTP content negotiation with an `Accept:` header specifiying your preferred format(s)
  - the tileset may contain additional useful information, such as the list of vector layers and properties schemas for vector tiles.
* Be aware of the tile matrix set in use based on either the `tileMatrixSetURI` (if available, for well-known TileMatrixSets) or the TileMatrixSet definition
  - use that information to determine the values and limits for {tileMatrix} {tileRow} {tileCol} and imply the geo-referencing of requested tiles accordingly
* If the `tileMatrixSetLimits` property exists in the tileset, avoid requesting tiles beyond those limits
* Use the URL template and substitute the {tileMatrix} {tileRow} {tileCol} variables by values to get a URL
  - get your tiles!

##### Styled Maps or Styled Vector tiles (e.g. for per-style scale-based filtering)
* If the service offers styled maps or styled vector tiles, follow rel: `styles` to obtain a list of styles from a landing page or collection, and discover links to tilesets from within the `styles` array inside that list of styles, using the `tilesets-*` relation types

### API approach
_WARNING: _OGC API - Tiles_ implementations are not required to use a `{tileMatrixSetId}` variable or offer local tile matrix set definitions, and TileSets URL templates are not required to follow a fixed path._

* Visit the API page directly
  - look for the /tileMatrixSets path (if local tile matrix set definitions and `{tileMatrixSetId}` are supported)
  - look for the /collections path (for tiles of a specific collections)
  - look for the /tiles or /collections/{collectionId}/tiles path (for vector tiles)
  - look for the /map/tiles or /collections/{collectionId}/map/tiles path (for map tiles)
  - look for the /collections/{collectionId}/coverage/map/tiles path (for coverage tiles)
  - look for the .../tiles/{tileMatrixSetId} path (if `{tileMatrixSetId}` is supported)
  - look for the .../tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol} path (if `{tileMatrixSetId}` is supported)
* Visit the /collections page (for tiles of a specific collections)
  - look for a collection of interest in the `collections` array and select an id (the `{collectionId}`).
* If the API supports a global list of TileMatrixSets and a `{tileMatrixSetId}`, visit `/tileMatrixSets` to select one
* Alternatively, discover the path to the tileset of interest from the API
* Access the tileset resource at e.g. /collections/{collectionId}/map/tiles/{tileMatrixSetId} and/or the tile matrix set definition at /tileMatrixSets/{tileMatrixSetId} to be aware of the TileMatrixSet in use
  - use that information to determine the values and limits for {tileMatrix} {tileRow} {tileCol} and imply the geo-referencing of requested tiles accordingly.
  - the tileset may contain additional useful information, such as the list of vector layers and properties schemas for vector tiles.
* If the `tileMatrixSetLimits` property exists in the tileset, avoid requesting tiles beyond those limits
* Use the .../tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol} template and substitute the variables by values to get a URL
  - get your tiles!

#### Styled Maps or Styled Vector tiles (e.g. for per-style scale-based filtering)
* If the service offers styled maps or styled vector tiles, replace .../map/tiles by .../styles/{styleId}/map/tiles (or .../tiles by .../styles/{styleId}/tiles), after having selected a style from those listed at .../styles.

### Selecting specific collections
* If an API or a collection contains data from multiple collections, use the `collections=` query parameter to select specific collections to be included in the tileset.
