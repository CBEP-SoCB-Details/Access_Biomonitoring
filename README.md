# Accessing Maine DEP's Biomonitoring Data

Maine's Department of Environmental Protection makes certain data available on-line 
at <https://www.maine.gov/dep/gis/datamaps/>.   Among those data, the site 
exposes GIS data on stream biomonitoring via a `KML` file, `lawb_biomonitoring.kml`.

`KML` files are used by (*inter alia*) Google Earth to represente geographic data.
At their heart, `KML` files are a specific flavor of `XML`, and they can be parsed
successfully by tools able to parse KML files.  Unfortunately, KML files are also
very flexible, and the data we are interested in finding can be buried in complex
ways.

The python code included in this repository is designed to parse data from KML
files and store the encoded information in spreadsheet-style tabular data.  The
code parses data from specific KML files produced and made available by Maine DEP.
The code for examines, unpacks, accesses and organizes data provided by DEP, as
wel las data accessible based on that data, by working our way back 
from the exposed KML files to various supporting files.

1. `KML` files are hierarchical, so that one `KML` file can refer to data embedded
   in other files in the internet.  In fact, the raw `KML` file DEP exposes (above)
   refers to several other files that contain the actual geographic data. The code
   hree works with those embedded files.  It is up to the user to download those
   additional KML files manually, following instructions in `README.md`, 
   `DATA_SOURCES.md`, and `DATA_NOTES.md` files.
   
2.  Closely related `KMZ` files are zip-encoded `KML` files, generally zipped along
    with related information, such as symbols used to diplay the geographic data. Again,
    when data is encapsulated in a KMZ file, users will need to "unzip" the files
    manually to work with the KML files enclosed within.

2. `KML` files can contain embeded data that is HTML (not XML) encoded. The default
   way that ArcGIS creates `KML` files apparently embeds the attribute table for each
   feature in an embedded `HTML` table. When we access attribute data, therefore, we 
   need te find and correctly parse an HTML table embeded within each (XML) "placemark"
   tag.

4.  Some related metadata and associated detailed data is contained in files not
    directly accessed via the KML files, but whose names can be inferred from the 
    attribute data.  Some code in this repository attempts to download files based on
    what appear to be DEP file naming conventions.

