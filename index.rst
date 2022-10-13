..
  Technote content.

  See https://developer.lsst.io/restructuredtext/style.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1



Introduction
============

The Rubin Observatory Science/System Requirements (LPM-17/LSE-29) and System Specifications (LSE-30) define the expected delivered image quality plus a breakdown of allocations of the contributions from various subsystems.  Some aspects/contributions to the system image quality are partially controllable/mitigated while others may be simply measurable.  Here we attempt to describe the operational plan for the observatory to effectively optimize the final system in Commission and Operations.


System-level Requirements
-------------------------


System contribution to seeing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Rubin design motivation is defined from the LPM-17 Science Requirements Document (SRD) and associated LSE-29 LSST System Requirements (LSR).  These requirements are mainly driven by weak lensing science, and use the theoretical Gaussian seeing model to convert between "seeing" and the "effective number of pixels" from an unresolved source.  The called out requirements define (at 3 fiducial atmospheric seeing values) the delivered median seeing across a single field of view (in r and i bands only) and limits of the fraction of images that exceed those specifications by a multiple factor.  This effectively constrains the error budget contribution from the final system to be between 0.3 (stretch) and 0.4 (minimal) arcseconds at zenith or contribute 10% to 15% to the final measurments (n_eff) and not exceed these limits for more than 10% of the field of view.  The degraded portions of the field shall have no more than root sum squared (RSS) measured contributions of 0.43, 0.46, and 0.52 in the first 3 seeing quartiles.  It should be noted that the allowed fraction of images that exceed all of these requirements are only included in particular ranges of atmospheric seeing (in quartile bins of the first 3 quartiles that are called out in the LSR and SRD and the 4th quartile seeing images are ignored for these requirements).  Away from zenith, this budget error will increase acordingly (by airmass to the 0.6 power), and for example for airmass of 2, be between an 0.45 and 0.59 arcsectond contribution.

Shape of point sources
~~~~~~~~~~~~~~~~~~~~~~

The spatial profile defines the shape of the point spread function (a double Gaussian) at 80%, 95%, and 99% enclosed energy radii (SR1, SR2, and SR3 for stretch, design, and minimum specification) at zenith, at a fiducial 0.69 arcsecond seeing in all bands and applies to the 10% fraction of images that exceed the previous error budget limits listed.  The median ellipticiy of "isolated bright point sources" is defined to be not larger 0.03 to 0.04 and no more than than 5% to 10% of the images should exceed 0.05 to 0.1 median ellipticity (also at 10 degrees zenith angle or less at a fiducial 0.69 arcsecond seeing).  The LSR further defines a limit for the fraction of images (15%) that the ellipticiy correlation function amplitude exceeds certain metrics (4e-5 for scales less than 5 arcminutes and 2e-7 for scales greater than 5 arcminutes).  The Observatory System Specifications (OSS, LSE-30) further defines a maximum ellipticty limit of 0.07 for to be exceeded by no more than 5% of images and relaxes the correlation amplitude for 10% of the images in the "main survey" or defined as acceptable for the main survey (4e-4 for scales less than 1 arcminute, 1e-6 for scales between 1 and 5 arcminutes and 5e-7 for scales greater than 5 arcminutes), and never to exceed 2e-4 for scales greater than 1 arcminute.  Also in the coadded survey (likly from the same set of images as defined before), the correlation amplitudes shall not exceed certain values (2e-5 for scales less than 1 arcminutes, 1e-7 for scales greater than 5 arcminutes, and smoothly vary in between without exceeding 2e-5).

Subsystem allocations
~~~~~~~~~~~~~~~~~~~~~

The OSS further breaksdown the image quality error budget contribution by subsystem.  The Camera cannot exceed a contribtion of 0.3 arcseconds, while the Telescope (and other parts of the observatory) is allocated 0.25 error contribution.  This flows down further into individual subsystems and is recorded in the image quality error budget (`LTS-124`_).

.. _LTS-124: http://ls.st/lts-124


Relevant elements of the system
-------------------------------

Camera
~~~~~~

The Camera is mounted within the optical "tube" or the telescope, so any temperature difference between the camera surfaces from ambient will cause convection in the surrounding air which would affect image quality.  This is controlled by circulating dynalene coolant through the camera (along with air circulation fans) that can operate on a servo loop with a set point based on temperature sensors internal to the camera.  The exact sensors to servo on and the target set point can be defined/redefined by the Rubin team in order match camera skin to the nominal ambient temperature.


Data Management
~~~~~~~~~~~~~~~

The Data Management (DM) system provides most of the data analysis code and the platform, the Rubin Science Platform (RSP), to perform the analysis.  The image data (and some associated metadata) is accessible via a postgress database, called "the Butler".  Most other telemetry (with a few exceptions) coming from other systems on the summit is stored in a separate timestream database, called "Engineering Facility Database".


Telescope and Site
~~~~~~~~~~~~~~~~~~

The Telescope and Site (T&S) consists of the remaining summit subsystems including the Dome, Mirrors, Telescope Mount Assembly (TMA), and support facility building plus the auxillary telescope observatory.  There are various environmental monitoring systems as well, including a dedicated weather station, air temperature, surface temperature, humidity, pressure, sky temperature, anemometers, accelerometers, and Differential Image Motion Monitors (DIMMs) deployed accross the summit site.  This system of components is collectively called the Environmental Awareness System (EAS) and also has control aspects to efficiently coordinate the reconfiguration of the observatory to optimize for image quality and observing efficiency.  Other relevant components of the T&S subsystem will be discussed later.


Image Quality Associated Measurements
=========================

Various EAS measurements are available via the EFD to link to image quality.

Air Temperature: ESS CSC, ~48 planned for MT, 5 for AT.  Product Owner Brian Stalder
-----------
The thermal stratification of the air inside the dome is perhaps the most critical factor for image quality in the dome seeing environment (other than the mirror temperature differentials, which are handled internally by each mirror cell). As such, the EAS must have a large array of air temperature probes. The full 3D air temperature structure also provides a critical crosscheck measurement that the venting system is working properly. In order to constrain and evaluate the thermal enviornment inside the dome, the EAS should have air temperature probes approximately every 5 meters of elevation, 7 around the circumference of the inside of the upper enclosure surface. This translates to about 28 probes. For the lower enclosure, a coarser spatial sampling will be utilized, as three elevations of five probes (four outside the pier and one inside) to match the geometry of the HVAC system. For the AuxTel, the EAS will provide five sensors inside the dome.


Surface Temperature: ESS CSC. ~58 planned for MT, 5 for AT.  Product Owner Brian Stalder
-------------------

The same type of temperature probes is utilized for surface/structural temperature. This sensing capability is necessary to verify that the major thermal masses inside the dome have reached equilibrium with the ambient environment. In addition, it is particularly critical for feedback on the Active Optics System to know the thermal state of the telescope mount in order to keep the optics properly aligned and focused. The EAS has provisioned approximately 58 additional structural probes (beyond what is provided by other subsystem components, such as the dome, TMA, M1M3, M2, and Camera) at various locations on the TMA, pier, upper and lower enclosure, and any other subsystem component determined to have a significant thermal influence on the dome environment


Anemomters and Turbulence Monitors: ESS CSC, 12 planned for MT, 1 for AT. Product Owner Brian Stalder
---------------------------

Another critical factor in image quality is to know the amount of air turbulence inside the dome environment. The flow of air around and through the dome will also provide critical feedback measurements to verify that the dome is optimally configured for scientific operations.  The EAS should have an array of 2D anemometers placed about every 15 meters along the surface inside the upper enclosure, particularly associated with the louver vents and dome slit aperture, for a total of 18 probes.

In order to disentangle the dome contribution to the image quality the EAS provides a direct measurement of the air turbulence inside the dome. This can be accomplished at specific points with 3D sonic anemometers.  An alternative to the sonic anemometer has been proposed, dubbed Dome Seeing Monitor. This apparatus is based on a design by Andrei Tokovinin, and implemented for the Dark Energy Camera on the Blanco Telescope that measures the motion of an artificial star beamed across a column of air that is directly proportional to the seeing turbulence in the air column.  The final configuration of 3D anemometers or Dome Seeing Monitors in the dome is still TBD.


External Conditions: Various CSCs, 1 on Calibration Hill, Product Owner Brian Stalder
-------------------

The weather station supplies most of the information of the external meterological conditions on the summit.  This includes temperature, wind, wind speed, humidity, and others.  A lightning localization system is also installed next to the dome.  There is also a rain, sky temperature, and daylight sensor mounted on the DIMM tower to allow for unattended/robotic operations.  These sensors' telemetry is also available.  There is also plans for a weather forecasting service, called meteoblue, to assist in predicting evening ambient temperature, cloud coverage, and atmospheric seeing.

Vibration: VMS CSC, 3 for MT (M1M3, M2, Camera), 1 for AT (truss).  Product Owner Doug Neill
---------

A critical feedback measurement of the EEC/EAS is to determine how much vibration is translated into the telescope and dome structure by the downdraft system. Also accelerometer data can measure the amount of wind buffeting the TMA can withstand.  Triaxial accelerometers mounted on the M1M3, M2, and Camera Rotator.  There is also the option to temporarily install additional accelerometers on other subsystems.  The raw timestream telemetry is stored in the large file annex section of the EFD, while a condensed summary, in an accumulated time window, is available via normal EFD database query.


DIMM and Direct Imaging: DIMM CSC, 1 on Calibration Hill, 1 is portable, Product Owner Brian Stalder
-----------------------

The ultimate feedback on the performance of the system is the delivered image quality of the science data. Other supplemental measurements of the image quality include the DIMMs (permanent and portable), and AuxTel.


Image Quality Available Control Aspects
=====================

The EAS is the central coordination between the various components of the observatory in order to configure it in real-time based on the environmental conditions.

Temperature Set Points: Various CSCs including MTMount, MTDome, EEC, M1M3, MTCamera.
----------------------

All major thermal heat sources in the dome shall be enclosed and actively cooled via either ethylene-glycol or dynalene.  The temperature target set points can be adjusted (individually) by the EAS to minimize air turbulence from convection off of hot surfaces.


Dome Louvers: MTDome CSC.
------------

During nighttime observing, the primary control of airflow through the dome will be accomplished by the dome louvers.  With a given windspeed and direction along with the azimuth of the target field, each of the 34 louvers should be configured to optimize air flushing versus wind buffeting the telescope.  This is estimated via CFD models to be around a 2.5 m/s uniform flow through the vents (and main aperture dome slit).

Downdraft System: EEC CSC.
----------------

In low wind conditions, air flow can be maintained with the support facility downdraft system which has a large ducted fan that pulls air down through the lower dome enclosure and exhaust through the far side of the building. 

Dome Air Conditioning: EEC CSC.
---------

During daytime operations, the heating of the dome by the sun is compensated by the 4 large air handling units in the lower enclosure.  The cooled air is ducted and forced up to the top of the upper dome enclosure to mechanically displace the hot air to avoid stratefication.  Note that this requires the dome be parked in a specific orientation for the ducts to line up, otherwise the cool air will exhaust at the 7th level platform instead of at the top of the dome.


Observation Scheduler: MTScheduler.
--------------

The feature-based scheduler drives the observations during the night in an effiecient manner.  The scheduler already includes an interface with a transparentcy map of the current sky, and has options to take other penalty/reward maps based on things like image quality, wind speed/direction, or other derived parameters.  These optional maps are to be defined.


Auxillary Telescope: Various CSCs.
------------

The auxillary telescope includes many aspects of the main telescope, and can be used as a testbed for experimental development and validation of algorithms.  It has a similar downdraft system (circulation fans) and a suite of EAS sensors.


Instrumentation
===============

As part of the EAS, a variety of sensors are in developement to provide situational information on the current state of the observatory.  These are summarized in the following table.

.. csv-table:: List of Sensors
	       :header: "Sensor Type", "# deployed", "# planned", "Model", "Product Owner", "Lead Dev", "CSC", "Notes"
			"Thermocouple","?","?","?","Stalder","Owen","ESS","M1M3, TMA, and Dome Deployment"
			"RTD","?","?","?","Stalder","Owen","ESS","Hexapods, Rotator, M2"
			"Accelerometers","3","4","?","?","Kubernek","VMS","TMA, M1M3, M2, Camera (rotator), 1 labjack prototype on AuxTel"
			"bi-axial anemometer","1","40","WINDSONIC1-L10-PW","Stalder","Owen","ESS","one on each of the louver banks, aperture shutter"
			"tri-axial anemometer","1","?","CSAT3B-NC","Stalder","Owen","ESS","unknown number/locations around the dome for turbulence"
			"DIMM","2","2","Astelco 12-inch","Stalder","Owen","DIMM","one permanently on calibration hill, one portable on tripod"


Other seeing sensors
--------------------

There are other sensors in prototyping and evaluation stages that are relevant to image quality.  Currently there are sensors deployed at AuxTel, by the Harvard IQ team and do not have any associated CSC with them with the possibile exception of those with a labjack-based readout.:

* Gill Instruments tri-axis device, model 1590, readout by a labjack
* Local seeing "strobed DIMM" prototype
* High-resolution differential temperature sensors
* Shack-Hartmann Camera on AuxTel Nasmyth

Plus there are two copies of a spot-motion monitor, invented by A. Tokovinin, but development on this has stalled after the first deployment due to Covid restrictions to the summit.



Operational Model
=================


Description of how a typical day/night will be executed.

Daytime
-------

The main operational mode for daytime is to condition the air inside the dome to reach the predicted ambient air temperature at the beginning of evening observations.  Deviations to that plan may come from daytime maintenance/engineering activities within the dome or of the HVAC system itself.  It is expected that normally the system can reach the target temperature in most situations, but it may be worthwhile to study what is the best course of action if the target temperature is not expected to be reached on a given day.  Possible options would be to open the dome early to expell hot air, additional pre-cooling (via lower set point) of the large themal masses, and/or operate the downdraft system to aid in flushing hot air.

Nighttime
--------

Three modes are envisioned based on wind speed/external condtions

Mode 1: Dome is fully closed at night due to bad weather or other causes; downdraft system is OFF.  HVAC maintains a target temperature of around the external ambient temperature (unless condensation is a risk) in case conditions improve.

Mode 2: Low wind: Dome louvers are all fully opened and downdraft system is ON. This mode will typically be selected when telescope is pointing directly into the wind, opposite to the wind, or the wind speed inside the dome is low.  Auxtel circulation fans set to appropriate speed.

Mode 3: High wind:  Same as Mode 2, but Downdraft system is OFF and Dome louvers on the upwind side are partially closed to reduce telescope windshake, or the wind speed inside the dome is too strong.  Scheduler may penalize observations directly into wind.  Auxtel circulation fans set to OFF, vents CLOSED.





Future Studies Needed
=====================

What is still unclear, unscoped, to be defined?

Investigation 1:  Measure dome seeing vs wind flushing, what is the optimum inside wind speed?  We can measure turbulence with sonic anemometers (or possibly other sensors?) in auxtel (and main telescope soon).

Investigation 2:  What is the nominal ambient temperature inside the dome?  Are there possible adjustments of set points to be done to make all surfaces as uniform as possible?  Auxtel doesn't have much control over this, so may have to wait to do this until system are installed in the main dome.

Investigation 3:  What do we do if evening temperature cannot be reached during the day?  

Investigation 4:  Impact of image quality vs windspeed/direction/louver configuration.  When do we close the louvers, start the downdraft, or avoid observing into wind?  What should be the penalty for observing close to the wind?  Can test this somewhat with auxtel (although no louvers).


   
.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
