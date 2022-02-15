========
Overview
========

NCAS Radar Data Standard
------------------------

NCAS currently operates a variety of radars as part of its programme of
observational science and facility provision.  These range in capabilty, some
incorporating scanning antennas, and some operating in fixed, zenith pointing
mode.  This document outlines the specification of a data standard developed for
NCAS radar data. It forms part of a wider standardisation of data formats for
NCAS observational data.  The guiding principles are those of FAIR (Findable
Accessible Interoperable Reusable) data management [FAIR2016]_.

There are now substantial drivers for data providers to implement the FAIR principles. These include:
The G20 group of nations: At the 2016 Hangzhou summit, the G20 leaders issued a statement endorsing the application of FAIR principles to research.
Increased emphasis on data and its reusability at policy level in national government and science funding bodies.
Science publishers have a grow0ing requirement for data DOI’s and data traceability.
The science community is expected to demonstrate data dissemination, usage, and deliver impact statements.

The FAIR principles of data management and stewardship aim to make data:

:Findable:
The first step in use and reuse data is to find them.
Metadata and data should be easy to find for both humans and computers.
Machine-readable metadata are essential for automatic discovery of datasets and services.

:This means:
Metadata are assigned a globally unique and eternally persistent identifier.
Data are described with rich metadata.
Metadata are registered or indexed in a searchable resource.
Metadata specify the data identifier.
:Accessible:
Once the user finds the required data, they need to know how they can be accessed, possibly including authentication and authorisation.
:This means:
Metadata are retrievable by their identifier using a standardised communications protocol.
The protocol is open, free, and universally implementable.
The protocol allows for an authentication and authorization procedure, where necessary.
Metadata are accessible, even when the data are no longer available
:Interoperable:
Data usually needs to be integrated with other data.
Data needs to interoperate with applications or workflows for analysis, storage, and processing.
:This means:
Metadata uses a formal, accessible, shared, and broadly applicable language for knowledge representation.
Metadata use vocabularies that follow FAIR principles.
Metadata include qualified references to other metadata.
:Reusable:
The ultimate goal of FAIR is to optimise the use and reuse of data.
To achieve this, metadata and data should be well-described so that they can be replicated and/or combined in different settings.
:This means:
Metadata have a plurality of accurate and relevant attributes.
Metadata are released with a clear and accessible data usage license.
Metadata are associated with their provenance.
Metadata meet domain-relevant community standards.

NCAS (https://www.ncas.ac.uk/) is putting its own house inorder and applying the FAIR principles to the data it generates. Working with the data scientists at CEDA (https://www.ceda.ac.uk/), the UK archive for atmospheric and earth observation data, the NCAS-Observation team have:
Defined data products for NCAS instrumentation.
Uniquely named all the NCAS instrumentation.
Developed an integrated repository structure for software and supporting documentation.
Introduced a controlled vocabulary for instruments and data products.
Introduced file standards that utilise the controlled vocabulary and are NetCDF4 - classic compliant.
The team is also working to produce various software tools which enable easy access to the data in these files. These tools are open-source and can be accessed via the NCAS-Observations website (https://sites.google.com/ncas.ac.uk/ncasobservations/home). The site also provides access to supporting information.

This document details what a user should expect to find in one of our data files. The first section of this document details the common file components and how they should be used: this includes how file names are constructed and the use of quality control flags. The second section details a common set of file level metadata (global and variable attributes and array dimensions) that appear in all files. i.e. irrespective of the data product. The final section details the data product specific metadata.

Note that:
Files will never include metadata (dimensions, global or variable attributes) that are not detailed in the data product supporting document.
If data for a common variable is not available then, these variables will be included but will contain only their designated  _FillValue.
If data for a data product specific variable is not available then, rather than pad the file with variables containing only the _FillValue, that variable will be omitted.

All the data files have the same file-level metadata irrespective of the instrument source. The file-level metadata components in each file are:
Global attributes: including the metadata standards followed in the file, change log (history) and other useful, general information (e.g. licence, authors etc):
Dimensions: information about the data array sizes. All data have a dimension of time
Variables: attributes of each data variable included in the file, e.g. name(s), units

Comment and feedback on the data file content, structure and supporting document is always welcome and appreciated. Please contact: barbara.brooks@ncas.ac.uk

This documents the wivern2_chilbolton is a collection of Python routines for processing the radar data collected during the WIVERN-2 ground-based observation campaign at Chilbolton Observatory in the UK.

These are the routines used to process raw (Level 0) time series data from the following radars:

* 3GHz CAMRa radar
* 35GHz Copernicus radar
* 94GHz Galileo radar

.. figure:: _static/example_data.png
	   :width: 500 px
	   :align: center

.. note::

    Near real-time Cloudnet data can be accessed at https://cloudnet.fmi.fi.


See also:

- Cloudnet data portal: https://cloudnet.fmi.fi/
- CloudnetPy source: https://github.com/actris-cloudnet/cloudnetpy
- ACTRIS home: http://actris.eu/
- ACTRIS data portal: http://actris.nilu.no/
