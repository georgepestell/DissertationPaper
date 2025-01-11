To enable this application to work efficiently on a wide variety of areas around the U.K, the modular feature design focused on enabling new features requiring accessing an API to be quickly implemented using a standardized procedure and helper functions.

There are many different types of features that can be created. Here, we will focus on the large category of features that require data to be fetched from an API.

There are different sub-categories of these types of features:
- direct-access RAW data
- process first, then access

Commonly, just tagging faces onto the topology is not sufficient to represent the depth of information stored in the API dataset. For example, large areas of grassland may have many different rivers and small ponds. If we only had representation of the edges of the terrain types, then the entire area would have to either be tagged as either water or land when tagging the water features.

Therefore, the feature creation is split into two processes: initialization, and preProcessing: initialization will fetch the data from the API, processing it, create constraints as required to represent the edges of features in the DTM, and cache the data if required for use in the pre-processing stage.

Different features will require different processing of the data to determine the constraints required to add to the DTM, but all will require the same process of fetching the data from the API, and converting the data to the UTM projected dataset (as the WGS84 is widely adopted for GIS datasets).

We therefore can simplify the process of creating a new feature using the following:
- create a `fetchDataFromApi` function which takes the mesh boundary, and fetches all of the required data from the API, parses it as a GDAL dataset, and warps it to the UTM projection. Returns a hashmap linking the WGS84 chunk to the dataset handle.
- create a `cacheDataset` function taking a hashmap linking WGS84 chunks to GDAL datasets, which will store each of the datasets provided into the cache.
Features can then use these datasets, modify them if required, and add constraints using the DTM as required.

Many features will not require any constraints to be added to the DTM, and many features won't require pre-processing.

When a Feature is created, it has access to the `fetchDataFromApi` function in the FeatureBase class. This acceepts the URL with the chunk latitude and longitude values to be marked with `{}` for the `fmt` formatter to fill. It uses the previously created UTM `MeshBoundary` object to determine the chunks, similarly to how the DEM data is fetched. It then downloads and parses the chunks from the API as GDAL datasets which can represent many different types of data. 




This data is stored in temporary files in storage, as often the memory usage would be unreasonably large for many data types. This data is then returned by the function as GDALDataset handles, allowing the user to process and cache the results if desired.