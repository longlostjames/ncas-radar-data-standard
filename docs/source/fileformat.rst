====================
Filename conventions
====================

Each radar file is named as

``<instrument_name>_<platform_name>_<date>-[<time>]_<scan_type>_[<option1>_<option2>_<option3>]_v<version>.nc``

==================
NetCDF conventions
==================

The NCAS-RADAR convention adheres to the CfRadial-1.4 format, and its subconventions.


Data types
All data conform to defined data types. Depending on the software used to interrogate the files data types may be given a different name to that used here. To be precise:

Python3 name
Definition
Range
byte
8-bit unsigned integer
0 to 255
int32
32-bit signed integer
-2,147,483,648 to +2,147,483,647
int64
64-bit signed integer
-9,223,372,036,854,775,808 to +9,223,372,036,854,775,807


float32
32-bit Single-precision floating-point
-3.4E+38 to +3.4E+38
float64
64-bit Double-precision floating-point
-1.7E+308 to +1.7E+308


Note the data type is not given as an explicit variable attribute.


Metadata (Global Attributes)
----------------------------

As the NCAS RADAR convention uses CfRadial-1.4 as its basis, all global
attributes required by the latter must be included.  The following global
attributes are required by CfRadial-1.4:

Conventions
   A space-delineated list of the conventions (and sub-conventions) that are
   followed by the dataset.  As NCAS-RADAR-1.0 uses version 1.4 of the CfRadial
   standard, this should be included explicitly. Sub-conventions such as
   "radar_parameters" are inherited from CfRadial-1.4, i.e. NCAS-RADAR-1.0 does
   not have a separate set of sub-conventions.

  :Example: NCAS-RADAR-1.0 CfRadial-1.4 instrument_parameters radar_parameters radar_calibration

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

  :Example:

instrument_name
  This should be filled with the unique NCAS instrument name

  :Example: ``ncas-mobile-x-band-radar-1``

The following global attributes are optional within CF/Radial-1.4, but are
required by NCAS-Radar-1.0:

platform_is_mobile

  :Example: false

The following global attributes are required by NCAS-Radar-1.0 but are not part
of the CfRadial-1.4 convention:

instrument_manufacturer
  The name of the instrument manufacturer

  :Example: ``Meteorologische Messtechnik (Metek) GmbH``

instrument_model
  The instrument model name

  :Example: MIRA-35

instrument_serial_number
  The instrument serial number which is registered to the instrument name used
  in the file name and linked to the “source”

  :Example: 63270V

instrument_pid
  This is a unique persistent identifier (PID) for the instrument, for example
  registered on the Handle.Net registry.  These PIDs are required when
  submitting data to the ACTRIS data centre, and so incorporating them here
  ensures correct cross-referencing.

  :Example: https://hdl.handle.net/21.12132/3.191564170f8a4686

instrument_software
  If known this is the name of the software running on the instrument that
  actually controls and makes the measurement.

  :Example: ``radar-camra-rec``

instrument_software_version
  Manufacturers often update instrument software and subtle changes in this
  code can result in changes in the quality of the data provided. To be able
  to trace any such effect the version of software running is embedded in the
  metadata.

  :Example: v2.08.11

creator_name
  This is the name of the person who generated the file. This is the person to
  contact if there are any questions about the data presented and how they were
  produced.

  :Example: A. Person

creator_email
  The contact email for the person who created the file. People move and this
  may not always be valid.

  :Example: A.Person@aplace.ac.uk

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

  :Example: v1.3

product_version
  Over time, errors or new calibrations means that the data may need to be
  reissued: they are the same data but just a different version. The version
  number is part of the file name and should match this value. Major revisions
  occur when a new calibration or processing method is applied while minor
  revisions occur to correct typos, etc. The reason for a the revision is
  detailed in the history field

  :Example: v<n.m> n - major revision, m - minor revision

processing_level
  This indicates the level of quality control that has been applied to the data.
  See the “Data Processing Levels” section for a full discussion.
  Options: 1, 2, or 3

last_revised_date
  This is the date of production of the data file. The time is UTC and is
  given in ISO format.

  :Example: 2013-06-06T12:00:00

project
  This is the full name and associated acronym of the project and should match
  that on official funding documents.

  :Example: Dynamics-aerosol-chemistry-cloud interactions in West Africa.
  (DACCIWA)

project_principal_investigator
  The name of the project Principal Investigator

  :Example: B. Person

project_principal_investigator_email
  Contact email for project PI

  :Example: B.Person@someplace.com

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
  field would be ``"christmas island”``. If the instrument was deployed on a
  ship called Oden then the value in this field would be ``“oden”``

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

  :Example: ``africa, ghana, kumasi, knust``

ncas_radar_vocabularies_release
  This is the url to the version controlled vocabulary used in defining the
  data file.  This is currently under development.



Global Variables
----------------

+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|**Name**                      |**Data type**  |**Dimension**            |Long name                                                                          |Units                                   |
+==============================+===============+=========================+===================================================================================+========================================+
| volume_number                | int           | none                    | | Volume numbers are sequential, relative to some arbitrary start time,           |1                                       |
|                              |               |                         | | and may wrap.                                                                   |                                        |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
| platform_type                | char          | (string_length)         | | Options are: *"fixed"*, *"vehicle"*, *"ship"*, *"aircraft"*, *"aircraft_fore"*, |none                                    |
|                              |               |                         | | *"aircraft_aft"*, *"aircraft_tail"*, *"aircraft_belly"*, *"aircraft_roof"*,     |                                        |
|                              |               |                         | | *"aircraft_nose"*, *"satellite_orbit"*, *"satellite_geostat"*                   |                                        |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|longitude                     |float32        |                         |longitude of the antenna                                                           |degree_east                             |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|height                        |float32        |                         |height of the elevation axis above mean sea level (Ordnance Survey Great Britain)  |m                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|frequency                     |float32        |                         |frequency of transmitted radiation                                                 |GHz                                     |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|prf                           |float32        |                         |pulse repetition frequency                                                         |Hz                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|beamwidthH                    |float32        |                         |horizontal angular beamwidth                                                       |degree                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|beamwidthV                    |float32        |                         |vertical angular beamwidth                                                         |degree                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|antenna_diameter              |float32        |                         |antenna diameter                                                                   |m                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|pulse_period                  |float32        |                         |pulse period                                                                       |us                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|transmit_power                |float32        |                         |peak transmitted power                                                             |W                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|clock                         |float32        |                         |clock input to ISACTRL                                                             |Hz                                      |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|range                         |float32        |range                    |distance from the antenna to the middle of each range gate                         |m                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|unaveraged_range              |float32        |unaveraged_range         |distance from the antenna to the middle of each range gate                         |m                                       |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|time                          |float32        |time                     |time                                                                               |seconds since 2020-09-22 00:00:00 +00:00|
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|dish_time                     |float32        |time                     |dish_time                                                                          |seconds since 2020-09-22 00:00:00 +00:00|
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|elevation                     |float32        |time                     |elevation angle above the horizon at the start of the beamwidth                    |degree                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|azimuth                       |float32        |time                     |azimuth angle clockwise from grid north at the start of the beamwidth              |degree                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|ZLO                           |short          |time, pulses, samples    |radar reflectivity factor low                                                      |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|ZHI                           |short          |time, pulses, samples    |radar reflectivity factor high                                                     |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|ZCX                           |short          |time, pulses, samples    |crosspolar radar reflectivity factor                                               |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|ITX                           |short          |time, pulses, samples    |TX I channel                                                                       |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|QTX                           |short          |time, pulses, samples    |TX Q channel                                                                       |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|IRX                           |short          |time, pulses, samples    |RX I channel                                                                       |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|QRX                           |short          |time, pulses, samples    |RX Q channel                                                                       |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+
|SPR                           |short          |time, pulses, samples    |Spare channel                                                                      |counts                                  |
+------------------------------+---------------+-------------------------+-----------------------------------------------------------------------------------+----------------------------------------+


Level 0a files
--------------

3GHz CAMRa time-series files
............................

These files are in NetCDF-3 format with the following content:

**Dimensions:**

+------------------------------+
|**Name**                      |
+------------------------------+
|time                          |
+------------------------------+
|range                         |
+------------------------------+
|unaveraged_range              |
+------------------------------+
|pulses                        |
+------------------------------+
|samples                       |
+------------------------------+

**Variables:**



**Global attributes:**

+--------------------------------+------------------------------------------------------------------------------+
|Name                            |Example                                                                       |
+================================+==============================================================================+
|radar                           |CAMRa                                                                         |
+--------------------------------+------------------------------------------------------------------------------+
|source                          |3-GHz Advanced Meteorological Radar (CAMRa)                                   |
+--------------------------------+------------------------------------------------------------------------------+
| | history                      | | Tue Sep 22 14:58:06 2020 - /usr/local/bin/radar-camra-rec \\               |
| |                              | | -fix 3600 115 90 -gates 5 201 -cellsize 1 -pulse_pairs 3050 -op rad \\     |
| |                              | | -id 0 -file 8030 -scan 7530 -date 20200922145806 -tsdump -tssamples 200    |
+--------------------------------+------------------------------------------------------------------------------+
|file_number                     |8030                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|scan_number                     |7530                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|scantype                        |Fixed                                                                         |
+--------------------------------+------------------------------------------------------------------------------+
|experiment_id                   |0                                                                             |
+--------------------------------+------------------------------------------------------------------------------+
|operator                        |rad                                                                           |
+--------------------------------+------------------------------------------------------------------------------+
|scan_velocity                   |0.f                                                                           |
+--------------------------------+------------------------------------------------------------------------------+
|min_range                       |-526.7335f                                                                    |
+--------------------------------+------------------------------------------------------------------------------+
|max_range                       |14088.15f                                                                     |
+--------------------------------+------------------------------------------------------------------------------+
|min_angle                       |90.f                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|max_angle                       |90.f                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|scan_angle                      |25.f                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|scan_datetime                   |20200922145806                                                                |
+--------------------------------+------------------------------------------------------------------------------+
|ADC_bits_per_sample             |12                                                                            |
+--------------------------------+------------------------------------------------------------------------------+
|samples_per_pulse               |196                                                                           |
+--------------------------------+------------------------------------------------------------------------------+
|pulses_per_daq_cycle            |6100                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|ADC_channels                    |8                                                                             |
+--------------------------------+------------------------------------------------------------------------------+
|delay_clocks                    |8                                                                             |
+--------------------------------+------------------------------------------------------------------------------+
|pulses_per_ray                  |6100                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|pulse_compression               |0                                                                             |
+--------------------------------+------------------------------------------------------------------------------+
|extra_attenuation               |0.f                                                                           |
+--------------------------------+------------------------------------------------------------------------------+
|radar_constant                  |64.7f                                                                         |
+--------------------------------+------------------------------------------------------------------------------+
|receiver_gain                   |45.5f                                                                         |
+--------------------------------+------------------------------------------------------------------------------+
|cable_losses                    |4.8f                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|year                            |2020                                                                          |
+--------------------------------+------------------------------------------------------------------------------+
|month                           |9                                                                             |
+--------------------------------+------------------------------------------------------------------------------+
|day                             |22                                                                            |
+--------------------------------+------------------------------------------------------------------------------+
|British_National_Grid_Reference |SU394386                                                                      |
+--------------------------------+------------------------------------------------------------------------------+

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




Level 0b files
--------------

3GHz CAMRa time-series files
............................

Level 0.5 files have been processed to remove redundant dimensions, and to make some changes to global attributes and variables.
The files are in NetCDF-4 format with the following content:

**Dimensions:**

+------------------------------+
|Name                          |
+==============================+
|time                          |
+------------------------------+
|range                         |
+------------------------------+
|pulses                        |
+------------------------------+


**Scalar Variables:**

+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|Name                          |Data type      |Dimension        |Long name                                                                            |Units                                   |
+==============================+===============+=================+=====================================================================================+========================================+
|latitude                      |float32        |none             |latitude of the antenna                                                              |degree_north                            |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|longitude                     |float32        |none             |longitude of the antenna                                                             |degree_east                             |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|altitude                      |float32        |none             |altitude of the elevation axis above mean sea level (Ordnance Survey Great Britain)  |m                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|frequency                     |float32        |none             |frequency of transmitted radiation                                                   |GHz                                     |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|prf                           |float32        |none             |pulse repetition frequency                                                           |Hz                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|beamwidthH                    |float32        |none             |horizontal angular beamwidth                                                         |degree                                  |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|beamwidthV                    |float32        |none             |vertical angular beamwidth                                                           |degree                                  |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|antenna_diameter              |float32        |none             |antenna diameter                                                                     |m                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|pulse_width                   |float32        |none             |pulse width                                                                          |us                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|transmit_power                |float32        |none             |peak transmitted power                                                               |W                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|clock                         |float32        |none             |clock input to ISACTRL                                                               |Hz                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|samples_per_pulse             |int            |none             |number of samples per pulse                                                          |1                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|pulses_per_daq_cycle          |int            |none             |number of pulses per data acquisition cycle                                          |1                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|pulses_per_ray                |int            |none             |number of pulses per ray                                                             |1                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|delay_clocks                  |int            |none             |clock cycles before sampling is initiated                                            |1                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|radar_constant                |float32        |none             |radar constant                                                                       |dB                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|receiver_gain                 |float32        |none             |receiver gain                                                                        |dB                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|cable_losses                  |float32        |none             |cable losses                                                                         |dB                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|extra_attenuation             |float32        |none             |extra attenuation introduced to receiver chain                                       |dB                                      |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+


**Coordinate Variables:**

+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|Name                          |Data type      |Dimension        |Long name                                                                        |Units                                   |
+==============================+===============+=================+=====================================================================================+========================================+
|range                         |float          |range            |distance from the antenna to the middle of each range gate                           |m                                       |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|time                          |float          |time             |time                                                                                 |seconds since 2020-09-22 00:00:00 +00:00|
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|elevation                     |float          |time             |elevation angle of antenna boresight above the horizon                               |degree                                  |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+
|azimuth                       |float          |time             |azimuth angle of antenna boresight clockwise from grid north                         |degree                                  |
+------------------------------+---------------+-----------------+-------------------------------------------------------------------------------------+----------------------------------------+

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



.ZLO_min    = -70.0,             /* dB       */
200	    .ZLO_scale  =   0.015625,        /* dB/count */
201	    .ZHI_min    = -38.0,             /* dB       */
202	    .ZHI_scale  =   0.015625,        /* dB/count */
203	    .ZCX_min    = -77.0,             /* dB       */
204	    .ZCX_scale  =   0.03125,         /* dB/count */
205	    .ZLO_thresh = 3840, /* 0x0F00 */ /* counts   */
206	    .Bias       = 2047, /* 0x07FF */ /* counts   */
207	    .ADCBits    = 12                 /* Bits     */

**Global attributes:**

+--------------------------------+--------------------------------------------------------------------------------------------------+
|**Name**                        |**Example**                                                                                       |
+================================+==================================================================================================+
|title                           |Time series from CAMRa collected for ESA WIVERN-2 campaign at Chilbolton Observatory (2020-2021)  |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|institution                     |National Centre for Atmospheric Science (NCAS)                                                    |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|instrument_name                 |ncas-radar-camra-1                                                                                |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|references                      |https://doi.org/10.1049/ecej:19940205; http://purl.org/net/epubs/work/63318                       |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|source                          |3-GHz Advanced Meteorological Radar (CAMRa)                                                       |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|history                         |Tue Sep 22 14:58:06 2020 - /usr/local/bin/radar-camra-rec -fix 3600 115 90                        |
+                                +-gates 5 201 -cellsize 1 -pulse_pairs 3050 -op rad -id 0 -file 8030                               +
|                                |-scan 7530 -date 20200922145806 -tsdump -tssamples 200                                            |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|comment                         |                                                                                                  |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|scantype                        |fixed                                                                                             |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|experiment_id                   |0                                                                                                 |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|operator                        |rad                                                                                               |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|time_coverage_start             |2020-09-22T14:58:06Z                                                                              |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|time_coverage_end               |2020-09-22T15:13:05Z                                                                              |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|pulse_compression               |false                                                                                                |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|ADC_bits_per_sample             |12                                                                                                |
+--------------------------------+--------------------------------------------------------------------------------------------------+
|ADC_channels                    |8                                                                                                 |
+--------------------------------+--------------------------------------------------------------------------------------------------+
