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


Science Requirements
--------------------

System contribution to seeing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Rubin design motivation is defined from the LPM-17 Science Requirements Document (SRD) and associated LSE-29 LSST System Requirements (LSR).  These requirements are mainly driven by weak lensing science, and use the theoretical Gaussian seeing model to convert between "seeing" and the "effective number of pixels" from an unresolved source.  The called out requirements define (at 3 fiducial atmospheric seeing values) the delivered median seeing across a single field of view (in r and i bands only) and limits of the fraction of images that exceed those specifications by a multiple factor.  This effectively constrains the error budget contribution from the final system to be between 0.3 (stretch) and 0.4 (minimal) arcseconds at zenith or contribute 10% to 15% to the final measurments (n_eff) and not exceed these limits for more than 10% of the field of view.  The degraded portions of the field shall have no more than root sum squared (RSS) measured contributions of 0.43, 0.46, and 0.52 in the first 3 seeing quartiles.  It should be noted that the allowed fraction of images that exceed all of these requirements are only included in particular ranges of atmospheric seeing (in quartile bins of the first 3 quartiles that are called out in the LSR and SRD and the 4th quartile seeing images are ignored for these requirements).  Away from zenith, this budget error will increase acordingly (by airmass to the 0.6 power), and for example for airmass of 2, be between an 0.45 and 0.59 arcsectond contribution.

Shape of point sources
~~~~~~~~~~~~~~~~~~~~~~

The spatial profile defines the shape of the point spread function (a double Gaussian) at 80%, 95%, and 99% enclosed energy radii (SR1, SR2, and SR3 for stretch, design, and minimum specification) at zenith, at a fiducial 0.69 arcsecond seeing in all bands and applies to the 10% fraction of images that exceed the previous error budget limits listed.  The median ellipticiy of "isolated bright point sources" is defined to be not larger 0.03 to 0.04 and no more than than 5% to 10% of the images should exceed 0.05 to 0.1 median ellipticity (also at 10 degrees zenith angle or less at a fiducial 0.69 arcsecond seeing).  The LSR further defines a limit for the fraction of images (15%) that the ellipticiy correlation function amplitude exceeds certain metrics (4e-5 for scales less than 5 arcminutes and 2e-7 for scales greater than 5 arcminutes).  The Observatory System Specifications (OSS, LSE-30) further defines a maximum ellipticty limit of 0.07 for to be exceeded by no more than 5% of images and relaxes the correlation amplitude for 10% of the images in the "main survey" or defined as acceptable for the main survey (4e-4 for scales less than 1 arcminute, 1e-6 for scales between 1 and 5 arcminutes and 5e-7 for scales greater than 5 arcminutes), and never to exceed 2e-4 for scales greater than 1 arcminute.  Also in the coadded survey (likly from the same set of images as defined before), the correlation amplitudes shall not exceed certain values (2e-5 for scales less than 1 arcminutes, 1e-7 for scales greater than 5 arcminutes, and smoothly vary in between without exceeding 2e-5).

Subsystem allocations
~~~~~~~~~~~~~~~~~~~~~

The OSS further breaksdown the image quality error budget contribution by subsystem.  The Camera cannot exceed a contribtion of 0.3 arcseconds, while the Telescope (and other parts of the observatory) is allocated 0.25 error contribution.  This flows down further into individual subsystems and is recorded in the image quality error budget (link/reference?).


Relevant elements of the system
-------------------------------


Hardware
========

Hardware details.

Software
========

Software details.

Operational Model
=================

Description of how a typical day/night will be executed.

Future Studies Needed
=====================

What is still unclear, unscoped, to be defined?
   
.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
