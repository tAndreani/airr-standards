============
Call 02/2020
============

------
Agenda
------

Follow-up
=========

*  Object definition for ``receptor`` and ``cell`` (in `#320`_, also
   see Christian's `comment in #273`__)
.. __ : https://github.com/airr-community/airr-standards/issues/273#issuecomment-568649516
*  List of To-Does for MiAIRR v2 in `#305`_
*  Should fields be non-nullable based on the availability of the
   information to the primary data depository (current situation) or
   the necessity of the information for meaningful interpretation?
   Note that the current situation can make it hard for third-party
   annotators `#310`_.

   *  A few things non-null "could" indicate:

      *  Criticality to MiAIRR as a Standard - things one MUST always
         have as decided by the AIRR Community.
      *  Things one should always be expected to have - not necessarily
         critical to MiAIRR but hard to understand how one could do a
         study and not have it.

   *  Note that many of the non-nullable fields are controlled
      vocabularies with ``NULL``-like options such as
      ``library_generation_method``:``other`` and
      ``physical_linkage``:``none``. Perhaps for non-nullable fields
      this should be the norm. We should consider carefully those fields
      that have limited possible values (booleans, controlled
      vocabularies with no null-like possibilities) and ensure that if
      they do not exist we really want that to data be not AIRR-
      compliant.

*  DataRep decision on ``organism`` field
*  Should we switch notes from Google Docs to Github?
*  Review `CEDAR Templates`_

   1. Confirm it is OK for the template, and the elements it is based
      on, to be publicly visible
   2. Confirm plan to have CEDAR's ``Version`` attribute not track
      MiAIRR version (which will be captured in title and description)


New Topics
==========

*  Use of x-airr attributes in specification `#297`_

   *  ``X-airr: required``
   *  How important is this to MiAIRR?

      *  Current understanding is that all MiAIRR fields are "required"
         but many can be ``NULL``. So when describing a study, the
         fields should always be present. There is discussion around
         the spec about making it possible to have a ``null`` object in
         the specification (e.g. ``Diagnosis``), which means that an
         AIRR Repertoire JSON file may not have all of the MiAIRR
         required fields (see `#328`_) (e.g. ``disease_diagnosis`` may
         not exist in the JSON description). From a specification of a
         study, this seems to make sense (if you do not have any
         diagnosis you do not have any of these fields) but from a
         MiAIRR perspective, the understanding is that it is desirable
         to have these fields present (for easier validation).

*  Split of ``read_length`` field (`#324`_ as fix for `#279`_ )

   *  Field ``read_length`` still exists, but its type has changed
      and it now is an integer and only represents read length in one
      direction.
   *  There is now a new ``paired_read_length`` field that is an integer
      that represents the read length in the paired direction.
   *  Field ``read_length`` was originally in the Schema object
      ``SequencingRun`` and in MiAIRR Set 3. In the new spec,
      ``read_length`` and ``paired_read_length`` are in the Schema
      object ``RawSequenceData`` as that is where the other ``paired_*``
      information (e.g., ``*direction`` or ``*filename``) is. This is
      Set 4. Currently, the ``x-airr`` tag for ``*read_length`` states
      Set 3, even though this is surrounded by Set 4 data.


-------
Minutes
-------


Meta
====

* Date: Fri, 2020-02-14 14:30 UTC
* Present: Ahmad, Brian, Christian, Florian, John


Follow-up
=========

*  DataRep deferred the decision on renaming ``organism`` species
   again, will bring it up again in March
*  Object definition ``cell`` and related data schema: Discussed at ComRepo
   call, Sri will go ahead with a schema and API implementation that
   initially will **not** support a tabular serialization (as it requires
   quite some nesting). Information on data schema can be found here:
   https://github.com/airr-community/airr-standards/issues/320#issuecomment-591416785
*  `CEDAR Templates`_: Confirmed that templates and their elements can be
   publicly visible (not requiring login). Also confirmed that CEDAR's
   version number can be distinct from MiAIRR version (assuming that
   it clearly labeled).
*  Switching to Github for agendas and minutes: Again no objections,
   starting test run for this call.
 
MiAIRR requirement levels
=========================

*  This is a combination of issues `#310`_ and `#297`_, which deal with
   nullable status of field, how to indicate this to users and how to
   represent it in the data schema.
*  We currently have three requirement levels (adopted from RFC2119)
   in table1_, where:

   *  "present" means that a field exists in a metadata description
   *  "NULL" means that a field has a ``NULL`` value (as in SQL) or a
      ``NULL``-like value that does also not provide any information on
      regarding this field. ``NULL``-like values are currently
      ``missing``, ``not applicable`` and ``not collected``, which were
      adopted from `BioSample attributes`_
   *  MiAIRR field are by default ``recommended`` as they are part of
      a minimal standard and thus MUST be present. Some MiAIRR fields
      might be ``required`` but never ``optional``

.. _`BioSample attributes`: https://www.ncbi.nlm.nih.gov/biosample/docs/attributes/

.. _table1:

+-----------------+-----------------+-------------+
| level           | MUST be present | CAN be NULL |
+=================+=================+=============+
| ``required``    | yes             | no          |
+-----------------+-----------------+-------------+
| ``recommended`` | yes             | yes         |
+-----------------+-----------------+-------------+
| ``optional``    | no              | yes         |
+-----------------+-----------------+-------------+

*  We agree that only fields that are essential for interpretation of
   data are ``required``, i.e., MUST NOT be NULL. This is different
   from the previous interpretation, which stated that all fields of
   which the information can be expected to be available to the data
   producer MUST be annotated. Further background in `#310`_ fixed
   by `#319`_.
*  Issues with the current terms for standard users:

   *  "required" does not implicate not being NULL
   *  "recommended" is misleading as the field MUST be present

*  Issues with the current representation in the AIRR Schema:
   OpenAPI knows a ``required`` and a ``nullable`` property, which
   potentially creates even more confusion as they have different
   meaning (``nullable`` only refers to ``NULL``, not to ``NULL``-like)
   and a different scope (``required`` would not only apply to the
   MiAIRR part of a field). This is discussed in `#297`_ and will 
   perspectively be fixed via `#319`_.
*  There will most likely never be perfect and 100% self-explanatory
   terms for the three levels, so documentation will be required.
   However, the potential confusion with OpenAPI should be resolved.
*  As the terms can be changed later on, we will try to find a reason-
   able set until the next call. All suggestions welcome.
   

New Topics
==========

``read_length`` field
---------------------

*  Moved ``*read_length`` to Set 4 in `#324`_, merged.
*  Strictly spoken, the addition of the other ``set: 4`` fields already
   broke compatibility as they are new requirements that were not
   present in AIRR v1.0. However ``set: 4`` is a dark place for MiAIRR
   anyhow, as it is just defined as raw data (i.e., not mandatory
   metadata, so in the real world nothing depends on this.
*  NCBI mapping needs to be updated, documented in `#330`_
*  Format change is could be relevant to CEDAR, who have noted this.


.. == Unlisted Links to AIRR Standards Github issues and pull requests ==

.. _`#279`: https://github.com/airr-community/airr-standards/issues/279
.. _`#297`: https://github.com/airr-community/airr-standards/issues/297
.. _`#305`: https://github.com/airr-community/airr-standards/issues/305
.. _`#310`: https://github.com/airr-community/airr-standards/issues/310
.. _`#319`: https://github.com/airr-community/airr-standards/pull/319
.. _`#320`: https://github.com/airr-community/airr-standards/issues/320
.. _`#324`: https://github.com/airr-community/airr-standards/pull/324
.. _`#328`: https://github.com/airr-community/airr-standards/issues/328
.. _`#330`: https://github.com/airr-community/airr-standards/issues/330

.. == Other Unlisted Links ==
.. _`CEDAR Templates`: https://openview.metadatacenter.org/templates/https:%2F%2Frepo.metadatacenter.org%2Ftemplates%2Fea716306-5263-4f7a-9155-b7958f566933
