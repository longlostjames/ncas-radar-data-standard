========
Overview
========

NCAS currently operates a variety of radars as part of its programme of
observational science and facility provision.  These range in capability, some
incorporating scanning antennas, and some operating in fixed, zenith pointing
mode.  This document outlines the specification of a data standard developed for
NCAS radar data. It forms part of a wider standardisation of data formats for
NCAS observational data.


---------------
FAIR Principles
---------------
The guiding principles for the NCAS Radar Data Standard are those of FAIR
(**F**\ indable **A**\ ccessible **I**\ nteroperable and **R**\ eusable) data
management :cite:p:`Wilkinson2016`.

A detailed description of the FAIR principles may be found at
https://go-fair.org/fair-principles/.
For ease of reference these are reproduced in part below.
The FAIR principles of data management and stewardship aim to make data:

**Findable**

The first step in (re)using data is to find them. Metadata and data should be
easy to find for both humans and computers.  Machine-readable metadata are
essential for automatic discovery of datasets and services.

This means:

* (Meta)data should be assigned a globally unique and persistent identifier.
* Data should be described with rich metadata.
* Metadata should clearly and explicitly include the identifier of the data
  they describe.
* (Meta)data should be registered or indexed in a searchable resource.

**Accessible**

Once the user finds the required data, they need to know how they can be
accessed, possibly including authentication and authorisation.

This means:

* Metadata are retrievable by their identifier using a standardised
  communications protocol.
* The protocol should be open, free, and universally implementable.
* The protocol should allow for an authentication and authorization procedure,
  where necessary.
* Metadata should be accessible, even when the data are no longer available

**Interoperable**

The data usually need to be integrated with other data.  In addition, the data
need to interoperate with applications or workflows for analysis, storage, and
processing.

This means:

* (Meta)data should use a formal, accessible, shared, and broadly applicable
  language for knowledge representation.
* (Meta)data should use vocabularies that follow FAIR principles.
* (Meta)data should include qualified references to other (meta)data.

**Reusable**

The ultimate goal of FAIR is to optimise the use and reuse of data.
To achieve this, metadata and data should be well-described so that they can be
replicated and/or combined in different settings.

This means:

* (Meta)data should be richly described with a plurality of accurate and
  relevant attributes.
* (Meta)data should be released with a clear and accessible data usage license.
* (Meta)data should be associated with detailed provenance.
* (Meta)data should meet domain-relevant community standards.


------
NetCDF
------

NCAS radar data products are provided in the **netCDF** format.
NetCDF (Network Common Data Form) is a set of software libraries and platform
independent data formats which are designed to support the creation, access,
and sharing of array-oriented scientific data. NetCDF is designed to be

* **Self-describing.** A netCDF file includes information about the data it
  contains (i.e. metadata).
* **Portable.** A netCDF file can be accessed by computers with different ways
  of storing integers, characters, and floating-point numbers.
* **Scalable.** A small subset of a large dataset may be accessed efficiently.
* **Appendable.** Data may be appended to a properly structured netCDF file
  without copying the dataset or redefining its structure.
* **Shareable.** One writer and many readers may simultaneously access the same
  netCDF file.
* **Archivable.** Access to all earlier forms of netCDF data will be supported
  by current and future versions of the software.

NetCDF is extremely commonly used, and is almost ubiquitous within the Earth
sciences. Unidata (https://unidata.ucar.edu) provide and maintain software
libraries for accessing netCDF data using C, C++, Java, and FORTRAN.
Third-party libraries (which are generally bindings or wrappers to the Unidata
libraries) are available for Python, IDL, MATLAB, R, Ruby, and Perl, among
others.

NetCDF files generally consist of four components:

* **Attributes:** Attributes are metadata that can be attached to the netCDF
  file itself (called global attributes), to variables, and to groups (variable
  attributes and group attributes, respectively). Attributes may be textual or
  numeric; numeric attributes may be arrays.
* **Groups:** Groups (available since netCDF4) provide a method to encapsulate
  related *dimensions,* *variables,* and *attributes*. They can be thought of as
  somewhat analogous to directories in a filesystem.
* **Dimensions:** Dimensions specify the size of a single axis of a variable
  within a netCDF file. Common dimensions for geophysical data include time,
  latitude, and longitude, though they do not need to correspond to physical
  dimensions. There is no practical limit to the number of dimensions which may
  be defined in a netCDF file.
* **Variables:** Variables are either scalar (single values pertaining the
  whole data set) or named *n*\ -dimensional arrays (thus associated with *n*
  *dimensions*) of a specified data type. Variables may have zero or more
  *attributes*, which act as metadata to describe the contents of the variable.

Radar data are typically recorded as time-stamped rays, each providing values of
an observable at a set of distances (ranges) from the radar.
Such so-called field variables are thus organised into 2-dimensional arrays,
along *time* and *range* dimensions.

Below is a minimal example in Python of accessing a 2-dimensional field
variable, *DBZH*, along with its *units* attribute and a global *title*
attribute from a netCDF file, is given below. Note that the netCDF library,
*netCDF4*, is not included as part of the Python standard library, but may be
installed using your system package manager, pip, or conda.

.. code-block:: python
    :linenos:

    from netCDF4 import Dataset

    with Dataset('some_radar_file.nc', 'r') as nc:
        title = nc.title
        DBZH_units = nc['DBZH'].units
        DBZH_data = nc['DBZH'][:]

This provides a simple means of inspecting the content of a radar field variable.
However, it takes no account of the spatial geometry.
To do this the user would need to read in additional variables describing the
range and the azimuth and elevation angles of the radar antenna.
To assist in standardising the way this is handled, the NCAS Radar Data Standard
draws on the CfRadial initiative (https://github.com/NCAR/CfRadial.git), and
currently uses
`CfRadial Version-1.4 <https://github.com/NCAR/CfRadial/blob/62cb351e16574baa9e7f2b54c6b93b13468077fb/docs/CfRadialDoc.v1.4.20160801.pdf>`_
as a base convention.

CfRadial has been developed as a CF-compliant netCDF format for radar and lidar
moments data in radial (i.e. polar) coordinates.
The intention is that the format should, as far as possible, comply with the
CF (Climate and Forecast) conventions (http://cfconventions.org/)
for gridded data. However, the current convention does not support radial
radar/lidar data. Therefore, extensions to the conventions are being proposed by
the developers of the CfRadial.

CfRadial is already supported by a number of community tools developed for
reading, visualizing, and analysing radar data.  These tools and software
environments include the
`Python ARM Radar Toolkit (Py-ART) <https://arm-doe.github.io/pyart/>`_,
the `Lidar and Radar Open Software Environment (LROSE) <http://lrose.net/>`_, and
`wradlib <https://docs.wradlib.org/en/stable/>`_, an open source library for
weather radar data processing.  Hence, there is a strong motivation for aligning
NCAS radar data with CfRadial in order to be able to allow users to employ some
of the most widely used software tools.


-------------
Usage License
-------------

NCAS radar data are licensed under the Open Government Licence
(http://www.nationalarchives.gov.uk/doc/open-government-licence).


See also:

- Centre for Environmental Data Analysis: https://ceda.ac.uk/
