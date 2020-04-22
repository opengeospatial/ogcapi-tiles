# Map Tiles

## How to get a map from a feature collection step by step

### Follow the links approach
* Visit the landing page
  - discover a link to collections
* Visit the /collections page
  - look for the list of {collectionId}s and select an id.
* Visit your favorite collection using /collections/{collectionId}
  - look for a link of rel='tiles'
* Visit the link of rel='tiles'
  - look for the 'links' property and select a 'link' with rel='item' (templated) and 'type' with the format you like
  - look for the 'styles' property with the list of stylesId's and select and id.
  - look for the 'tileMatrixSetLink' property to know about the TileMatrixSetId values
* if the TileMatrixSetId is unknown
  - look for the 'tileMatrixSetURI' in the 'tileMatrixSetLink' property to figure out the values and limits on {tileMatrix} {tileRow} {tileCol}.
* if the 'tileMatrixSetLimits' property exists in the 'tileMatrixSetLink'
  - tune the values of {tileMatrix} {tileRow} {tileCol} accordingly
* Use the URL template and substitute the variables by values to get a URL
  - get your tile!

### API approach
* Visit the API page directly
  - look for the /collections path
  - look for the /collections/{collectionId}/map/tiles path
  - look for the /collections/{collectionId}/map/{styleId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol} path
* Visit the /collections page
  - look for the list of {collectionId}s and select an id.
* Visit the /collections/{collectionId}/map/tiles page
  - look for the 'styles' property with the list of stylesId's and select and id.
  - look for the 'tileMatrixSetLink' to know about the TileMatrixSetId
* if the TileMatrixSetId is unknown look for the /tileMatrixSets/{tileMatrixSetId}' in the  page and figure out the values and limits on {tileMatrix} {tileRow} {tileCol}.
* if the 'tileMatrixSetLimits' property exists in the 'tileMatrixSetLink'
  - tune the values of {tileMatrix} {tileRow} {tileCol} accordingly
* Use the /collections/{collectionId}/map/{styleId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol} template and substitute the variables by values to get a URL
  - get your tile!
