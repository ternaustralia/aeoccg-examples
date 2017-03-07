# Accessing TERN AusCover Data on the NCI and RDS <br>

<center><table>
<tr>
<!--td><a href='http://www.tern.org.au'><img src='http://tern.org.au/rs/7/sites/998/custom_files/tpl_images/logo.jpg'></a></td-->
<td><a href='http://www.auscover.org.au'><img src='http://qld.auscover.org.au/logo.png'></a></td>
<td><a href='http://www.nci.org.au'><img src='https://www.wpcentral.com.au/wp-content/uploads/2013/08/nci-logo1.png' width="200"></a></td>
<td><img src='http://nci.org.au/wp-content/uploads/2015/05/Official-RDS-Logo-RGB.png' width="200"></td></tr>
</table></center>

#### A Technical Capacity Building Webinar for AEOCCG

_Presented by [Peter Scarth](mailto:p.scarth@uq.edu.au?subject=AEOCCG%20webinar%20information) (Joint Remote Sensing Research Program) with lots of help and input from Kelsey Druken and Claire Trenham from the [NCI](http://nci.org.au/about-nci/contact/nci-staff-2/)._

### Abstract

Have you ever wondered how to access some of the TERN AusCover remotely sensed data which is available on the NCI using some of the available web services directly within your analysis environment?

This webinar will give several examples using direct access using opendap on thredds and gdal/rasterio on thredds and http where you'll be able to query and directly interact with Landsat, MODIS and Himawari datasets in both  iPython notebooks and in GIS packages. By the end of the webinar, you’ll be able to discover some of the many data sets openly available  on the NCI and query them using web services.

#### Background on RDS <> TERN AusCover <> NCI <> AGDC?
 - [TERN AusCover](http://auscover.org.au) - provides a national expert network and a data delivery service for provision of Australian biophysical remote sensing data time-series, continental-scale map products, and selected high-resolution datasets over TERN sites. **It is a virtual network for earth observation data sets across Australia that are typically produced by universities, state government agencies _(e.g. NSW OEH and Qld DSITI)_, and federal  agencies _(e.g. GA, BOM and CSIRO)_ ).**
 - [Research Data Storage Infrastructure (RDSI)](https://www.rds.edu.au) - supports collaborative access to research data assets of national significance (including national reference collections) through distributed data centre development. **They provide the online storage capacity to host Australian EO data sets online.**
 - [National Computational Infrastructure (NCI)](http://nci.org.au/) -  is Australia’s national research computing facility including the Southern Hemisphere’s most highly-integrated supercomputer and filesystems, Australia’s highest performance research cloud, and one of the nation’s largest data catalogues. **They provide the compute capacity for some of the Auscover data sets, interactive environments, and cataloging and training services.** 
 - [Australian Geoscience Data Cube (AGDC)](http://www.datacube.org.au/) - provides an integrated gridded data analysis environment for earth observation satellite and related data from multiple satellite and other acquisition systems. **This project facilitates the operational processing and interactive  analysis of national EO data sets and is used to produce the Landsat and MODIS collections on the NCI.**

These groups work together to improve the processing, storage, cataloging, discovery and analysis of EO based data across Australia.

#### The NCI VDI
Data downloading and analysis by many users has potential risks _(apart from the data being too big for this to be feasible!)_. **Bringing scientists to the data can help mitigate these issues by ensuring everyone is working on the same data.** To support this workflow, the NCI runs a Virtual Desktop Environment with:
 - Tools to support climate data analysis & visualisation
 - Virtual laboratory to access, process & analyse data
 - Analyses input data in a consistent format 
 - Workflow tools allow science community to                                        implement own analyses without dealing directly with filesystems & HPC
 - A range of standard software tools connected to the global Lustre filesystem and HPC
 -  Desktops: 32GB RAM, 140GB local scratch, 8vCPUs
 - [How can I get VDI access?](http://nci.org.au/access/getting-access-to-the-national-facility/allocation-schemes/ )

### NCI and RDS TERN AusCover Services

NCI have a multi-element system for metadata catalogues and data services
 - [GeoNetwork](http://geonetwork.nci.org.au): Find metadata records (akin to CSIRO DAP)
 - [THREDDS](http://dap.nci.org.au) Data Service: download or remotely access or view data
   - OPeNDAP is one of the protocols served, permits subsetting and remote access to files
   - Other protocols include HTTP download and Open Geospatial Consortium Web Services to stream JPEG, TIFF etc.
 - Geoserver, ERDDAP, Hyrax, others… and filesystem
 - PROMS (provenance), DOI minting (citation)

[TERN AusCover](http://qld.auscover.org.au/public/html/index.html) also uses [THREDDS](http://qld.auscover.org.au/thredds/catalog.html),  [Geoserver](http://qld.auscover.org.au/geoserver/web/), [FTP](ftp://qld.auscover.org.au/) and [HTTP](http://qld.auscover.org.au/public/data/) services to deliver data in a variety of formats, and is working to refine online discovery,  subsetting and reformatting tools for both raster and vector data. Keep an eye out for the new website launching soon.


## Presentation Outline

For these examples I'll be using a [Jupyter Notebook](http://jupyter.org/) with code in Python.
 - _The Jupyter Notebook is a web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text and has support for over 40 programming languages, including Python, R, Julia and Scala_. 
 - If you've never used Jupyter Notebooks before, I highly recommend installing [Anaconda](https://www.continuum.io/downloads)
 - _As an aside, many of the packages used by JRSRP and partners, such as [RIOS](http://rioshome.org/), [RSGISLIB](http://www.rsgislib.org/) and [PyLidar](http://pylidar.org/) can be installed into this environment from the [OSGEO Conda index](https://conda.anaconda.org/osgeo)_

This notebook will outline some simple online interaction with some of the **JRSRP Landsat seasonal mosaics**. We'll treat the data hosted on http://qld.auscover.org.au as files and use the [RasterIO](https://www.mapbox.com/blog/rasterio-announce/) package to interact with the data and undertake some typical remote sensing tasks. Finally we'll build a simple example to extract and analyse a time series of imagery across an agricultural research property in the Burdekin (from ~5 TB of raster data hosted online).

Then we'll look at how you'd **access some of the GA Landsat data** produced out of the AGDC and hosted on the NCI using the OPeNDAP protocol via THREDDS. [Link to Hosted Notebook](https://github.com/nci/Notebooks/blob/master/Python_Examples/Python_GDAL_NetCDF.ipynb)

Finally we'll check out a pretty cool notebook that uses the NCI THREDDS Data Server and queries the **CSIRO Auscover MODIS** data sets to extract a time series of imagery. [Link to hosted Notebook](https://github.com/nci/Notebooks/blob/master/Data_Access/Using_Siphon/Python_Siphon_II.ipynb)


### Additional NCI Resources

We won't have much time to look at how you query and explore the THREDDS catalog to [access data](https://github.com/nci/Notebooks/blob/master/Data_Access/Using_Thredds/THREDDS_DataAccess.ipynb) or find [WMS and WCS service endpoints](https://github.com/nci/Notebooks/blob/master/Data_Access/Using_Thredds/THREDDS_WMS_WCS.ipynb) so I'd strongly encourage you to follow these links if you want to find out more.

Similarly, **accessing many of these data sets is easy using your desktop GIS package**. This will be the topic of another TERN AusCover session later in the year, but for now have a look at the [NCI QGIS examples](https://github.com/nci/Notebooks/tree/master/QGIS_Examples).


This all looks a little more tricky than firing up your desktop remote sensing package, but you do get a highly flexible open source analysis environment that give you the ability to perform reproducible research, and operationalise your algorithms nationally with ease.
See the links below for training information, more Jupyter notebooks or NCI help:
 - https://training.nci.org.au 
 - https://github.com/nci/Notebooks
 - http://nci.org.au/user-support/getting-help/
