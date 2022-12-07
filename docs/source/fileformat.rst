====================
Filename conventions
====================

Each radar file is named as

``<instrument_name>_<platform_name>_<date>-[<time>]_<scan_type>_[<option1>_<option2>_<option3>]_v<version>.nc``

==================
NetCDF conventions
==================

The NCAS-Radar convention has at its heart the CfRadial format, and its
subconventions.  CfRadial is a comprehensive specification, and we only
discuss required elements here. For more complex use, e.g. for pulsed radar
systems with complicated pulsing schemes, the user should consult the full
CfRadial documentation, which may be found on Github at
``https://github.com/NCAR/CfRadial``.

Version 1.0 of the NCAS-Radar standard is based on CfRadial-1.4.


.. rubric:: Strict variable and attribute names for non-field variables

CfRadial requires strict adherance to naming conventions for dimensions and for
non-field variables.  By the latter we mean variables such as *time*, *range*,
*azimuth* and *elevation*, and other variables containing metadata such as
calibration offsets.  The NCAS-Radar convention inherits this requirement.
For details see the CfRadial documentation on Github.

Overview of data content
========================
The data fields containing observables from a radar instrument, i.e. the
moments of the Doppler velocity spectrum are produced over a time or angular
interval at a sequence of ranges increasing radially away from the instrument.
The term "ray" is used to refer to a set of range gates at a given time or angle.
In most cases the spacing between range gates is constant along a ray, but this
is not compulsory.

Data fields are typically stored as 2-D arrays, with dimnesions **(time,range)**.
This is typical for NCAS radars where each ray has the same number of gates.
CfRadial does allow for the more general case where rays have a variable number
of gates.  For details see the CfRadial documentation.

In addition to the **time** and **range** dimensions, CfRadial introduces a third
"pseudo"-dimension, which allows the field data to be subdivided into so-called
"sweeps".  For example, a single constant elevation PPI scan constitutes an
example of a sweep, and a typical NetCDF data file will have a **volume** that
comprises one or more such sweeps.  The convention uses start and stop indices
to identify which rays belong to a given sweep.  Also, some rays may contain
data collected during the transition between sweeps, and these are indicated
using an "antenna_transition" flag.



Metadata (Global Attributes)
============================

Attributes required by CfRadial-1.4
-----------------------------------
As the NCAS-Radar-1.0 convention uses CfRadial-1.4 as its basis, all global
attributes required by the latter must be included.  The following global
attributes are required by CfRadial-1.4:

Conventions
   A space-delineated list of the conventions (and sub-conventions) that are
   followed by the dataset.  As NCAS-Radar-1.0 uses version 1.4 of the CfRadial
   standard, this should be included explicitly. Sub-conventions such as
   "radar_parameters" are inherited from CfRadial-1.4. NCAS-Radar-1.0 does
   not have a separate set of sub-conventions.

  :Example: ``NCAS-Radar-1.0 CfRadial-1.4 instrument_parameters radar_parameters radar_calibration``

title
  This is a short description of the file contents.

  :Example: ``Moments from the NCAS Mobile X-band Radar unit 1 at Sandwith, UK``

institution
  This is the name of the institution employing the creator.  This is added to
  help users of the data track down the creator if they need to.

  :Example: ``National Centre for Atmospheric Science (NCAS)``

references
  References that describe the data or the methods used to produce it.
  For example, this may be a paper describing the instrument.

  :Example: ``https://doi.org/10.5194/amt-11-6481-2018``

source
  This is a descriptor that uniquely identifies the source of the original data.

  :Example: ``NCAS Mobile X-band Radar unit 1``

history
  This is freeform text that gives the history of the data from collection to
  the present version.

comment
  This is free form text and is used to provide the user with any additional
  information that may be of use.

instrument_name
  This should be filled with the unique NCAS instrument name

  :Example: ``ncas-mobile-x-band-radar-1``

Attributes required by NCAS-Radar-1.0 that are optional in CfRadial-1.4
-----------------------------------------------------------------------
The following global attributes are optional within CfRadial-1.4, but are
required by NCAS-Radar-1.0:

platform_is_mobile

  :Example: ``false``

Additional attributes required by NCAS-Radar-1.0
------------------------------------------------
The following global attributes are required by NCAS-Radar-1.0 but are not part
of the CfRadial-1.4 convention:

instrument_manufacturer
  The name of the instrument manufacturer

  :Example: ``Meteorologische Messtechnik (Metek) GmbH``

instrument_model
  The instrument model name

  :Example: ``MIRA-35``

instrument_serial_number
  The instrument serial number which is registered to the instrument name used
  in the file name and linked to the “source”

  :Example: ``63270V``

instrument_software
  If known this is the name of the software running on the instrument that
  actually controls and makes the measurement.

  :Example: ``radar-camra-rec``

instrument_software_version
  Manufacturers often update instrument software and subtle changes in this
  code can result in changes in the quality of the data provided. To be able
  to trace any such effect the version of software running is embedded in the
  metadata.

  :Example: ``v2.08.11``

creator_name
  This is the name of the person who generated the file. This is the person to
  contact if there are any questions about the data presented and how they were
  produced.

  :Example: ``A. Person``

creator_email
  The contact email for the person who created the file. People move and this
  may not always be valid.

  :Example: ``A.Person@aplace.ac.uk``

creator_url
  The ORCID URL of the person who created the file is something that goes with
  them and unlike email using this to trace the creator has a greater chance of
  success.  Other PIDs may be used, but ORCID is the preferred option.

  :Example: ``https://orcid.org/0000-0000-0000-0000``

processing_software_url
  To go from the Level 0 data produced by the source to the files archived
  requires the creator to do some sort of data processing. This processing may
  involve various levels of QC and data formatting so that it meets the archive
  standard. Where this code is developed by the creator it is deposited on an
  open repository - usually GitHub - and this is the url to that code. The use
  of a repository means that the code is version controlled and the exact
  version used to create the file is accessible.

  This only applies to creator-developed code - no manufacturer proprietary
  software is ever deposited in the repository

  :Example: ``https://github.com/name1/name2/``

processing_software_version
  This is the version of the processing software.

  :Example: ``v1.3``

product_version
  Over time, errors or new calibrations means that the data may need to be
  reissued: they are the same data but just a different version. The version
  number is part of the file name and should match this value. Major revisions
  occur when a new calibration or processing method is applied while minor
  revisions occur to correct typos, etc. The reason for a the revision is
  detailed in the history field

  :Example: ``v2.1``

processing_level
  This indicates the level of quality control that has been applied to the data.
  See the “Data Processing Levels” section for a full discussion.
  Options: ``1``, ``2``, or ``3``

last_revised_date
  This is the date of production of the data file. The time is UTC and is
  given in ISO format.

  :Example: ``2013-06-06T12:00:00``

project
  This is the full name and associated acronym of the project and should match
  that on official funding documents.

  :Example: ``Microbiology-Ocean-Cloud-Coupling in the High Arctic (MOCCHA)``

project_principal_investigator
  The name of the project Principal Investigator

  :Example: ``B. Person``

project_principal_investigator_email
  Contact email for project PI

  :Example: ``B.Person@someplace.com``

project_principal_investigator_url
  ORCID URL or other persistent identifier of the PI.

  :Example: ``https://orcid.org/0000-0000-0000-0000``

licence
  The UK Government Licensing Framework (UKGLF) provides a policy and legal
  overview of the arrangements for licensing the use and re-use of public sector
  information, both in central government and the wider public sector. It sets
  out best practice, standardises the licensing principles for government
  information, mandates the Open Government Licence (OGL) as the default
  licence for Crown bodies and recommends OGL for other public sector bodies.

  :Example: ``Data usage licence - UK Open Government Licence agreement: http://www.nationalarchives.gov.uk/doc/open-government-licence``

acknowledgement
  Obtaining and producing these data represents a substantial amount of effort
  and investment of resources. It is expected that users of these data
  acknowledge this by following the request directive given in this field.

  :Example: ``Acknowledgement of NCAS as the data provider is required whenever and wherever these data are used``

platform
  The platform is the site or mobile platform where the instrument was deployed.
  For example if it was deployed at Christmas Island then the value in this
  field would be ``christmas island``. If the instrument was deployed on a
  ship called Oden then the value in this field would be ``oden``

time_coverage_start
  This is the time value of the first ray of data in the file. The time is UTC
  and in ISO format.  Note that CfRadial-1.4 also incorporates this as a global
  string variable.  Including it here as a global attribute aligns with usage
  in data files from other NCAS instruments.

  :Example: ``2013-02-01T00:00:00Z``

time_coverage_end
  This is the time value of the last ray of data in the file. The time is UTC
  and in ISO format. Note that CfRadial-1.4 also incorporates this as a global
  string variable.  Including it here as a global attribute aligns with usage
  in data files from other NCAS instruments.

  :Example: ``2013-03-31T23:59:59Z``

geospatial_bounds
  For a stationary platform this is just the latitude and longitude part
  (signed decimal). For a moving_platform it is the geographic bounding box
  geospatial_lat_min geospatial_lon_min, geospatial_lat_max geospatial_lon_max
  (signed decimals),  The main purpose of this field is to aid data discovery.

  :Example 1: ``-111.29N 40.26E``
  :Example 2: ``Bounding box: -111.29N  40.26E, -110.29N  41.26E``

platform_altitude
  This is the altitude above the WGS84 geoid of the ground at the point of
  deployment. All instrument deployment heights are given with respect to this.
  Where altitude is a variable this is given with respect to the WGS84 geoid
  and not with respect to the local ground.

  :Example: ``263m``

location_keywords
  These are words with geographical relevance that aid data discovery.

  :Example: ``cumbria, sandwith``

Optional (but recommended) attributes in NCAS-Radar-1.0
-------------------------------------------------------

instrument_pid
  This is a unique persistent identifier (PID) for the instrument, for example
  registered on the Handle.Net registry.  These PIDs are required when
  submitting data to the ACTRIS data centre, and so incorporating them here
  ensures correct cross-referencing.

    :Example: ``https://hdl.handle.net/21.12132/3.191564170f8a4686``


Dimensions
==========

As mentioned above, the naming of these dimensions must adhere strictly to the
CfRadial-1.4 requirements.


+------------------------------+-----------------------------------------+
|**Dimension name**            |**Description**                          |
+==============================+===============+=========================+
| time                         | The number of rays. This dimension is   |
|                              | optionally unlimited.                   |
+------------------------------+-----------------------------------------+
| range                        | The number of range bins                |
+------------------------------+-----------------------------------------+
| sweep                        | The number of sweeps                    |
+------------------------------+-----------------------------------------+
| string_length [#f1]_         | Length of char type variables           |
+------------------------------+-----------------------------------------+

.. [#f1] Any number of ‘string_length’ dimensions may be created and used. For
   example, you may declare the dimensions ‘string_length', ‘string_length_short’
   and ‘string_length_long’, and use them appropriately for strings of
   various lengths. These are only used to indicate the length of the strings
   actually stored, and have no effect on other parts of the format.


Global Variables
================

Variables named in **bold** in the following table are required by Cf-Radial-1.4
and NCAS-Radar-1.0.  Others are optional.

+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**Name**                 |**Data type**  |**Dimension**          |**Comments**                                                                       |**Units**                               |
+=========================+===============+=======================+===================================================================================+========================================+
| **volume_number**       | int           | none                  | | Volume numbers are sequential, relative to some arbitrary                       |1                                       |
|                         |               |                       | | start time, and may wrap.                                                       |                                        |
+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| platform_type           | char          | (string_length)       | | Options are: *"fixed"*, *"vehicle"*, *"ship"*, *"aircraft"*, *"aircraft_fore"*, |none                                    |
|                         |               |                       | | *"aircraft_aft"*, *"aircraft_tail"*, *"aircraft_belly"*, *"aircraft_roof"*,     |                                        |
|                         |               |                       | | *"aircraft_nose"*, *"satellite_orbit"*, *"satellite_geostat"*                   |                                        |
+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| **time_coverage_start** | char          | (string_length)       | | UTC time of first ray in file. Resolution is integer seconds. The               | none                                   |
|                         |               |                       | | time(time) variable is computed relative to this time.                          |                                        |
|                         |               |                       | | Format is yyyy-mm-ddThh:mm:ssZ                                                  |                                        |
+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| **time_coverage_end**   | char          | (string_length)       | | UTC time reference. Resolution is integer seconds. If defined,                  | none                                   |
|                         |               |                       | | the time(time) variable is computed relative to this time instead of            |                                        |
|                         |               |                       | | relative to time_coverage_start. Format is yyyy-mm-ddThh:mm:ssZ                 |                                        |
+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| time_reference          | char          | (string_length)       | | UTC time of last ray in file. Resolution is integer seconds.                    | none                                   |
|                         |               |                       | | Format is yyyy-mm-ddThh:mm:ssZ                                                  |                                        |
+-------------------------+---------------+-----------------------+-----------------------------------------------------------------------------------+----------------------------------------+

Coordinate Variables
====================

Variables in the following table are required by Cf-Radial-1.4 and
NCAS-Radar-1.0.

+-------------------------+---------------+---------------------------+
|**Name**                 |**Data type**  |**Dimension**              |
+=========================+===============+===========================+
| **time**                | double        | (time)                    |
+-------------------------+---------------+---------------------------+
| **range**               | float         | (range) or (sweep,range)  |
+-------------------------+---------------+---------------------------+

Attributes for the time coordinate variable
-------------------------------------------

+-------------------------+---------------+---------------------------------------------------+
|**Name**                 |**Type**       |**Value**                                          |
+=========================+===============+===================================================+
| **standard_name**       | string        | "time"                                            |
+-------------------------+---------------+---------------------------------------------------+
| | **long_name**         | | string      | | "time_in_seconds_since_volume_start" or         |
| |                       | |             | | "time_since_time_reference"                     |
+-------------------------+---------------+---------------------------------------------------+
| | **units**             | | string      | | "seconds since *yyyy*-*mm*-*dd*T*hh*:*mm*:*ss*Z"|
| |                       | |             | | where the actual reference time values are used.|
+-------------------------+---------------+---------------------------------------------------+
| calendar                | string        | Defaults to "gregorian" if missing.               |
+-------------------------+---------------+---------------------------------------------------+

Attributes for the range coordinate variable
--------------------------------------------

+--------------------------------------+---------------+---------------------------------------------------+
|**Name**                              |**Type**       |**Value**                                          |
+======================================+===============+===================================================+
| **standard_name**                    | string        | "projection_range_coordinate"                     |
+--------------------------------------+---------------+---------------------------------------------------+
| | **long_name**                      | | string      | | e.g. "range_to_measurement_volume" or           |
| |                                    | |             | | "range_to_middle_of_each_range_gate"            |
+--------------------------------------+---------------+---------------------------------------------------+
| **units**                            | string        | "metres" or "meters"                              |
+--------------------------------------+---------------+---------------------------------------------------+
| **spacing_is_constant**              | string        | "true" or "false"                                 |
+--------------------------------------+---------------+---------------------------------------------------+
| | **meters_to_center_of_first_gate** | | float or    | Start range                                       |
| |                                    | | float(sweep)|                                                   |
+--------------------------------------+---------------+---------------------------------------------------+
| | meters_between_gates               | | float or    | | Gate spacing.  Required if spacing_is_constant  |
| |                                    | | float(sweep)| | is "true"                                       |
+--------------------------------------+---------------+---------------------------------------------------+
| **axis**                             | string        | "radial_range_coordinate"                         |
+--------------------------------------+---------------+---------------------------------------------------+

Location Variables
==================

+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**Name**                      |**Data type**  |**Dimension**            |**Comments**                                                                       |**Units**                               |
+==============================+===============+=========================+===================================================================================+========================================+
|**latitude**                  |double         |none or (time)           |Latitude of the instrument                                                         |degree_north                            |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**longitude**                 |double         |none or (time)           |Longitude of the instrument                                                        |degree_east                             |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| |**altitude**                | | double      | | none or (time)        | | Altitude of the instrument above the geoid.  For a scanning radar this is the   | | metres or meters                     |
| |                            | |             | |                       | | altitude of the elevation axis.                                                 | |                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+

Sweep Variables
===============

Sweep variables are always required, even if the volume only contains a single sweep.

+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**Name**                      |**Data type**  |**Dimension**            |**Comments**                                                                       |**Units**                               |
+==============================+===============+=========================+===================================================================================+========================================+
|**sweep_number**              |int            |(sweep)                  |The number of the sweep in the volume scan, starting at 0.                         |                                        |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| | **sweep_mode**             | | char        | | (sweep,string_length) | | Options are "sector", "coplane", "rhi", "vertical_pointing", "idle",            | |                                      |
| |                            | |             | |                       | | "azimuth_surveillance", "elevation_surveillance", "sunscan", "pointing",        | |                                      |
| |                            | |             | |                       | | "manual_ppi", "manual_rhi"                                                      | |                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**fixed_angle**               | float         |(sweep)                  | Target angle for the sweep.                                                       | degree                                 |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**sweep_start_ray_index**     | int           |(sweep)                  | Index of the first ray in sweep relative to the start of volume. 0-based.         |                                        |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**sweep_end_ray_index**       | int           |(sweep)                  | Index of the last ray in sweep relative to the start of volume. 0-based.          |                                        |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+

Moments Field Data Variables
============================

Field data variables

Data Quality Flags
The data provided will have had some level of processing performed upon: be that instrument or post processing averaging, motion correction, or the variable may be derived from such core variables. These concepts were introduced in section 3. The quality of the data is provided via the Data Quality Control Flag. This flag is a mask and represents the provider's considered opinion. Data users can apply the mask to the data or not - it is the user's choice. By taking this approach, the data provided is of greatest versatility.

A file containing just one data quality flag will contain the variable qc_flag. Where a  file contains more that on data quality flag variable the data quality flag named is structured as:  qc_flag_<name>
qc_flag_temperature
qc_flag_relative_humidity
qc_flag_pressure
qc_flag_wind
qc_flag_radiation
qc_flag_precipitation

Flag variables are always of data type byte and are defined such that they have the same dimensions as the variables they are associated with: there is a flag value associated with every data point. They all follow a standard structure with the following attributes:
units
Definition: Units of a variable’s content. Where a variable is unit less the value 1 is used.
Example: 1
long_name
Definition: Long descriptive name which is often used for labelling plots
Example: Data Quality flag: Temperature
flag_values
Definition: Values the data flag can have
Example: 0b, 1b, 2b, 3b
flag_meanings
Definition: How the flag should be interpreted
Example:
not_used
good_data
suspect_data_unspecified_instrument_performance_issues_contact_data_originator_for_more_information
Suspect_data_time_stamp_error

To reflect the fact that what affects data quality can vary, the flag_values and flag_meanings are not rigidly tied down. That is they may vary on a file-by-file basis. What does not vary is the structure and the usage: the qc_flag variable is structured and used so that for every flag_value there is a corresponding flag_meaning. In this standard we use an integer value in the range 0 to n (being of data type byte the maximum value of n is 255):
0 is reserved for future use and is not used
1 is always good data.

Consider the variable air_temperature which has data:
-20
-3
-2
-1
-2
-3
-2
-1
0
-1
0
2
3
4
2
3
20
4
3
2

While qc_flag_temperature has data:
3
1
2
1
1
1
1
1
1
1
1
1
1
2
1
1
3
2
1
1

The flag_values attribute is “0b, 1b, 2b, 3b” and the flag_meanings attribute gives:
not_used
good_data
suspect_data_unspecified_instrument_performance_issues_contact_data_originator_for_more_information
Bad_data_value_outside_instrument_measurement_range

If the user wanted only to see “good” data (indicated by a qc_flag value of 1) all they would need to do would be to:
Make a copy of the variable data array
Set the value of the elements in the duplicate data array that correspond to elements on the qc_flag that have a value not equal to 1 to NaN.
This will result in the temporary data variable looking like:
NaN
-3
NaN
-1
-2
-3
-2
-1
0
-1
0
2
3
NaN
2
3
NaN
NaN
3
2


If the user wanted to accept “suspect” data in addition to “good” data (indicated by a qc_flag value of 1 and ) all they would need to do would be to:
Make a copy of the variable data array
Set the value of the elements in the duplicate data array that correspond to elements on the qc_flag that have a value not equal to 1 or 2 to NaN.
This will result in the temporary data variable looking like:
NaN
-3
-2
-1
-2
-3
-2
-1
0
-1
0
2
3
4
2
3
NaN
4
3
2







**Field Variables**

+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|Name                          |Date type      |Dimensions               |Long name                                                                    |Units                                   |
+==============================+===============+=========================+=============================================================================+========================================+
|ZLO                           |short          |time, pulses, range      |radar equivalent reflectivity factor low                                     |dBZ                                     |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|ZHI                           |short          |time, pulses, range      |radar equivalent reflectivity factor high                                    |dBZ                                     |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|ZCX                           |short          |time, pulses, range      |crosspolar radar equivalent reflectivity factor                              |dB                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|ITX                           |short          |time, pulses, range      |in-phase video signal on transmission                                        |1                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|QTX                           |short          |time, pulses, range      |quadrature video signal on transmission                                      |1                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|IRX                           |short          |time, pulses, range      |in-phase video signal on reception                                           |1                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+
|QRX                           |short          |time, pulses, range      |quadrature video signal on reception                                         |1                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------+----------------------------------------+

Field variables are stored in packed form of type ``short`` and have the following attributes:

+----------------------------------------+------------------+
|Attribute name**                        |Type*             |
+========================================+==================+
|scale_factor                            |float32           |
+----------------------------------------+------------------+
|add_offset                              |float32           |
+----------------------------------------+------------------+
|valid_min                               |short             |
+----------------------------------------+------------------+
|valid_max                               |short             |
+----------------------------------------+------------------+
|_FillValue                              |short             |
+----------------------------------------+------------------+

For example for ``ZLO`` the packed values derive from the analogue to digital
converter, and lie in the range ``[0,4095]``.
The attribute ``valid_max`` is set to ``3840``, and only values below this
threshold should be used.

Similarly ``ZHI`` has the attribute ``valid_min`` set to ``3841``, and only
values above this should be used.
