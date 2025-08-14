# Guidance on Establishing IDAC Data Transfer Channels

## Abstract
Independent Data Access Centers (IDACs) will be receiving large amounts of data with each data release from the US Data Facility (USDF). The primary mechanism intended for managing these transfers is through Rucio. We provide guidance on establishing Rucio Storage Endpoints (RSEs) based on pre-DP1 data transfer tests carried out with IDAC teams.

## Introduction
As described in [RTN-003](http://ls.st/rtn-003), IDACs and Scientific Processing Centers (SPCs) offer computing resources (CPU, GPU, storage) and (for IDACs) access to subsets of Rubin LSST data, that augment the resources available at the US Data Access Center. A requirement for this distributed computing network to work is the ability to perform bulk data transfers, as described in [RTN-086](http://ls.st/rtn-086), between the USDF and the receiving IDACs. Since data transfers will typically occur before data is released to the community, IDACs must also be aware of and abide by Rubin's pre-release data policy, described in [RDO-121](http://ls.st/rdo-121).

This document is intended to serve as a rough guide for implementing bulk data transfers. It was developed through initial experiments with data transfers to the IDACs in Canada and Poland in early 2025.

## Summary
As described in [RTN-086](http://ls.st/rtn-086), data transfers from USDF to other sites are done using [Rucio](https://rucio.cern.ch/). To enable these, receiving sites must set up compatible storage, set up endpoints to that storage, and provide authentication and authorization certificates after agreeing to Rubin's pre-release data policy and being added to Rubin's LSST Virtual Organization. The creation of the Rucio Storage Elements and initiation of data transfers are done on the Rubin USDF side.

## Rucio Storage Element Configuration
Rucio requires that specific storage technology be utilized in order to support the deployment of an RSE. [RTN-032](https://rtn-032.lsst.io/#specification-of-rucio-storage-element-rse) details requirements in more specificity (in the context of multi-site processing operations). Present RSEs have been configured utilizing [EOS](https://eos-web.web.cern.ch/eos-web/) and [dCache](https://www.dcache.org/), while [XRootD](https://xrootd.org/) is also known to be supported.

Once the correct storage technology is available, a storage endpoint may be configured. Examples of existing storage endpoints include:
- Canada
  - URL: `https://eos-mgm-0.keel-dev.arbutus.cloud:8443/eos/keel-dev.arbutus.cloud/data/lsst`
  - Storage Technology: EOS v5.3 (XrootD/5.7.2)
  - RSE Name: `IDAC_CAN-CAN`
- Poland
  - URL: `https://se.cis.gov.pl:2880/grid/lsst`
  - Storage Technology: dCache/9.2.21
  - RSE Name: `IDAC_POL-NCB`

Storage endpoints should be named according to the convention IDAC_+ [the in-kind program identifier](https://www.lsst.org/scientists/in-kind-program/programs), e.g.:
- Australia: IDAC_AUS-AAL
- Brazil: IDAC_BRA-LIN
- Canada: IDAC_CAN-CAN
- Croatia: IDAC_CRO-RBI
- Denmark: IDAC_DEN-IDA
- Japan: IDAC_JAP-JPG
- Mexico: IDAC_MEX-UNA
- Poland: IDAC_POL-NCB
- Slovenia: IDAC_SLO-UNG
- Spain: IDAC_ESP-BCM
- South Korea: IDAC_KOR-KAS
- UK: IDAC_UKD-UKD


## Authorization
As part of the requirements listed in [RDO-121](http://ls.st/rdo-121), each IDAC must have designated technical staff members who have filled out the [Staff Access Form](https://ls.st/staff-access-form) and be added to the LSST VO. Upon signing the Staff Access Form, IDAC personnel should notify Knut Olsen and/or Sierra Villarreal, who will notify the Rubin Ops Director.

Additionally, each IDAC must provide a description of their plans for Authentication and Authorization (A&A), needed to ensure abidance by Rubin data rights policies. Example A&A plans include the following:
- [Brazilian A&A Plan](https://docs.google.com/document/d/1okCcgxymznAPxqbcnoEcM6wUJhpMHEna0iZP98NdHPs/edit?tab=t.0)

Upon approval, a Rubin staff member will add the IDAC technical staff contact to the [LSST VO](https://github.com/opensciencegrid/osg-vo-config/tree/master).

SLAC VOMS server details are as follows:
- Server Endpoint: `voms.slac.stanford.edu:15003`
- Configuration Files: `https://voms.slac.stanford.edu:8443/voms/lsst/configuration/configuration.action`

USDF staff will handle setting distances from SLAC and the relevant rules in Rucio to facilitate transfers.

## Checklist
To be ready to accept bulk data transfers via Rucio, each IDAC should provide:
- A list of all technical and programmatic points of contact.  The technical point of contact should include the person (or people) who have filled out the Staff Access Form.
- A statement of how the IDAC indends to comply with the pre-release data-handling policy described in [RDO-121](http://ls.st/rdo-121).
- A statement of how the IDAC will implement data-rights controls consistent with [RDO-013](http://ls.st/rdo-013).
- Verification that a test data distribution to the IDAC-based Rucio Storage Element completed successfully.
