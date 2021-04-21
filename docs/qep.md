# QGIS Enhancement: Replace core support for QGIS GeoNode integration with a plugin

**Date** 2021/MM/DD

**Author** Kartoza

**Contact** info at kartoza dot com

**Maintainer** @ricardogsliva @samweli

**Version** QGIS 3.20

# Summary

QGIS GeoNode integration helps to view, browse and load resources from GeoNode instances
into QGIS.

The QGIS GeoNode integration achieved its intended goals, but still it lacked some important functionalities when
accessing the GeoNode data, 
for example 

1. The integration only support reading the data, data upload to GeoNode is not available.
2. Private layers can't be accessed through the GeoNode provider. 
3. No support for authentication.
4. Management for layers metadata and styles is not available.


[qgis/QGIS#4816](https://github.com/qgis/QGIS/pull/4816)

[qgis/QGIS#42783](https://github.com/qgis/QGIS/pull/42783)


## Proposed Solution
While the integration core implementation added a GeoNode QGIS provider it still
used OGC services ( WMS, WFS and WCS(added recently)) to access and add the GeoNode data inside QGIS, this make it
questionable whether it is necessary to have core implementation for the GeoNode provider acting as intermediate
layer between QGIS and OGC services, or the same could be achieved with a dedicated QGIS plugin and hence decouple 
QGIS core with the GeoNode specific code.

We are recommending using a QGIS plugin that will replace the core implementation for the QGIS GeoNode integration. 
The plugin will introduce new important missing functionalities in the core implementation, it will leverage the GeoNode API V2
to achieve this, the recently added API offers a range of features in accessing the GeoNode data.

The main aim is to improve the QGIS GeoNode integration in such a way that management of GeoNode data can be done inside
QGIS. That is, QGIS can be easily used to access, create, upload and delete data inside GeoNode instances.

The following functionalities will be included in the plugin GeoNode provider.

1. Support for loading layers with metadata, it will be possible to view GeoNode layer metadata inside QGIS.
2. Access of private layers via QGIS authentication system, the new API V2.
3. Providing search filters when searching for resources.
4. Management of layers, which include access, upload and deletion of the GeoNode layers.

The plugin will not make any changes on the current QGIS browser behaviour, service and layer access through
the QGIS browser will remain the same.

The plugin will still support old versions of GeoNode that doesn't have the new API V2.


### Example(s)
https://kartoza.github.io/qgis_geonode/

### Affected Files

[qgis/src/providers/geonode](https://github.com/qgis/QGIS/tree/master/src/providers/geonode)

## Performance Implications

Improved GeoNode layers search and loading times. 

## Backwards Compatibility

Only QGIS 3.20 and later will be supported.

All GeoNode versions will be supported

## Issue Tracking ID(s)
[kartoza/qgis_geonode](https://github.com/kartoza/qgis_geonode/issues)

[qgis/QGIS#42761](https://github.com/qgis/QGIS/issues/42761)
