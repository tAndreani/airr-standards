====================
MiniStd Call 09/2019
====================

------
Agenda
------

Decisions
=========

*  Changes to the "Age" field to accommodate for age ranges (`#192`_)


Follow-up
=========

*  Subdomain for CAIRR at airr-community.org


New topics
==========

*  General handling of quantities with ranges and different units
*  Geographical locations: How to annotate country level information?
*  Should relations between subjects be moved into ``Study``?


-------
Minutes
-------

Meta
====

*  Date: Fri, 2019-09-13 13:30 UTC
*  Present: Ahmad, Brian, Christian, Florian, Francisco, John, Marcos,
   Sri


Decisions
=========

*  The replacement of the field ``age`` with ``age_min``, ``age_max``
   and ``age_unit`` was **approved**. This considered to be a change in
   data representation, not in content, thus it will enter the standard
   in AIRRv1.3.


Follow-up
=========

*  Subdomain for CAIRR: The subdomain cairr.airr-community.org has been
   approved by ExCom. Brian has setup the domain, but still needs a URL
   to redirect to.


New topics
==========

*  General handling of quantities with ranges and different units: We
   will use `#192`_ as an example in the docs on how to handle ranges
   and multiple units for a field.
*  We agreed that adding country information regarding place of birth
   (``Subject``) and place of sampling (``Sample``) would be a valuable
   addition. Will look into encoding of this information and MiAIRR
   status and discuss again in `MiniStd Call 10/2019`_.
*  Should relations between subjects be moved into ``Study``: While
   there was a consensus that this would simplify working with more
   complex relationships (e.g. grand-parents to grand-children), there
   was also doubt whether there is a real need for change at this point.
   Therefore it was decided to shelf this topic for now, but
   nevertheless create a ticket to document it (`#308`_).


====================
MiniStd Call 10/2019
====================

------
Agenda
------

Follow-up
=========

*  Subdomain for CAIRR at airr-community.org


New topics
==========

*  Inclusion of species information for cell and locus annotations
   (`#137`_)
*  Human population genetics extension, a proposed more generalized
   implementation of the country level information discussed during
   `MiniStd Call 09/2019`_.


-------
Minutes
-------

Meta
====

*  Date: Fri, 2019-10-11 13:30 UTC
*  Present: Ahmad, Brian, Christian, Florian, Francisco, John, Sri

Follow-up
=========

*  The CAIRR subdomain [http://cairr.airr-community.org] is now live and
   the recommended way to link to CAIRR in AIRR-C manuscripts, docs,
   etc. Technical info: This is done via a HTTP 302 redirect.

New topics
==========

*  Inclusion of species information for cell and locus annotations
   (`#137`_): Cells and nucleic acids in a sample might not be of
   ``organism`` origin (e.g., BM chimeric mice or animals with human Ig
   loci as transgenes). To allow for annotation of this information, we
   plan to introduce the ``cell_species`` and ``locus_species`` fields.
   The fields will be OPTIONAL, i.e., they do not have to be present,
   which is in contrast to other MiAIRR fields that MUST be present, but
   CAN contain a NULL-like value. Please leave comments in `#260`_ until
   the next call.
*  Human population genetics extension (`#264`_):

   *  MiAIRR currently contains a number of fields that do not
      necessarily meet the stringent definition for being "minimal",
      i.e. being independent of the experimental design of a study (e.g.
      are subjects humans?). To prevent potentially erroneous or
      misleading annotation for the sake of "standard compliance", it
      seems appropriate to move such fields out of the core standard and
      into separate extensions (XTs). These will then be required to be
      used in a modular fashion if certain conditions are met by a
      study. This will also solve (some) of the issues related to a
      single field requiring multiple ontologies, depending on the
      context.
   *  Suggestion is to nove the following fields, which are rather
      specific for human populations, into a "Human Population Genetics"
      extension. If currently present, the fields will be removed from
      the core standard in AIRRv2.0.

      *  ``ancestry_population``
      *  ``ethnicity``
      *  ``race``
      *  ``country_birth`` (defined in `#265`_)
      *  ``collection_country`` (defined in `#265`_ )
   

====================
MiniStd Call 11/2019
====================

------
Agenda
------

Follow-up
=========

*  Species information for cell and locus annotations (`#137`_)
*  Rename MiAIRR field "Organism" to "Species" (`#266`_)
*  Human Population Genetics XT (`#264`_)


-------
Minutes
-------

Meta
====

*  Date: Fri, 2019-11-08 14:30 UTC
*  Present: Ahmad, Brian, Christian, Florian, Francisco, John, Sri


Decisions
=========

*  Inclusion of species information for cell and locus annotations
   (`#137`_) was **approved**.

   *  Introduction of the fields ``cell_species`` and ``locus_species``,
      will be added to the schema via `#260`_.
   *  Principle of "layering" (i.e. specialized keys deeper down in in
      the schema hierachy can override more general definitions of the
      same feature that took place further up) will be added to the
      docs.


Follow-up
=========

*  Rename "Organism" to "Species":

   *  The designation for this field is formally incorrect as an
      organism is an individual of a species, not the species itself.
      However, it is the latter one that we are aiming to annotate in
      this field. This could lead to confusion when using the term as a
      suffix (e.g., `#137`_). The current term is derived from the
      `INSDC Feature Table`_, which uses rather creative semantics to
      make it fit.
   *  There is a consensus that the MiAIRR name should be changed. As
      this breaks compatibility it will be slated for inclusion in
      AIRRv2. Whether the key ``organism`` will be changed at the same
      time, is up for discussion with with DataRep (`#266`_).

*  Human Population Genetics XT: We will get feedback from GLDB WG in
   their November call. The proposal will be put to a vote in
   `MiniStd Call 12/2019`_, please comment on Github (`#264`_, `#265`_).


New topics
==========

*  Documentation of effective changes to the standard/schema: While
   nearly all changes made to the standard over the last two years are
   documented in some Github ticket, there is no comprehensive log that
   would summarize all changes. DataRep will discuss how they think this
   can be done with creating too much overhead.
*  Deprecation vs. renaming of fields: While we have a procedure to
   document deprecation of fields (`#248`_), it is unclear how to
   document renaming, especially how to keep the information what the
   new field name is.
*  Relation between MiAIRR Set 6 and DataRep ``Rearrangement``:

   *  This has been an area of overlapping responsibility for some time.
      Although it has not been an issue until now that two WG basically
      define similar items, it is probably time to get this sorted out.
   *  As DataRep is the larger stakeholder, the proposal is that they
      set the standard definition for rearrangement data (e.g, as
      published in [Vander_Heiden_2018]_). The MiAIRR "Set 6" would then
      be described as the subset of rearrangement fields from the
      DataRep standard that are recommended as the minimal information
      that one should store in INSDC repositories. For these fields,
      MiniStd will provide a mechanism for mapping the data to the
      `INSDC Feature Table`_.
   *  Essentially, DataRep becomes the owner/definer of rearrangement
      data fields. MiniStd would no longer define these fields, but it
      would identify a subset of the rearrangement fields defined in the
      DataRep standard that it considers minimal via the inclusion of
      these fields into MiAIRR Set 6. In addition, implementations of
      MiAIRR would provide a mechanism/procedure for mapping those
      minimal rearrangement fields to the INSDC repositories.
   *  DataRep will discuss this on Monday.

*  John: Are there current statistics on how many AIRR data sets are
   available via SRA/Genbank/TLS? No, Christian will collect these
   numbers for the next call.


====================
MiniStd Call 12/2019
====================

------
Agenda
------

Follow-up
=========

*  Current NCBI submission stats
*  Rename MiAIRR field "Organism" to "Species" (`#266`_)
*  Inclusion of species information for cell and locus annotations
   (`#260`_)
*  Human Population Genetics XT (`#264`_, `#265`_)
*  DataRep Discussion (`#248`_):

   *  How to document changes to the standard in a transparent fashion?
   *  How to document renaming (instead of deprecation) of fields?

*  Relationship between MiAIRR Set 6 and DataRep ``rearrangement``
   object
*  Adding gene and gene family to DataRep spec but not MiAIRR (`#258`_)
*  Talking about a Spec definition for cell (`#211`_)


-------
Minutes
-------

Meta
====

*  Date: Fri, 2019-12-13 14:30 UTC
*  Present: Brian, Christian, Corey, Francisco, Florian, Marcos, Sri


Decisions
=========

*  Renaming "Organism" field to "Species" was **approved**. After we
   discussed this again, the renaming was put to a vote. It was decided
   to perform this renaming in the upcoming v2 release of MiAIRR and the
   AIRR schema (see `#266`_).
*  Relation between MiAIRR Set 6 and DataRep ``rearrangement``. See
   minutes of `MiniStd Call 11/2019`_ for a summary. DataRep is fine
   with the suggested procedure (DataRep governs the fields, MiniStd
   simply declares whether a field is "minimal" in terms of reporting).
   We **approved** this as the new mode of operation, which will be
   included in the documentation until the v2 release, although it is
   formally independent of it.


Follow-up
=========

*  Human Population Genetics XT: Due to time restrictions this was not
   yet brought up in a GLDB call. Therefore comments on the respective
   tickets (`#264`_, `#265`_) were requested via the GLDB mailing list
   until our next call.
*  Makeing renaming of fields trackable: Renaming (not only deprecation)
   is now included `#248`_ and defined as a To-Do for v2.0 (`#305`_).
*  Addition of further gene call fields to ``rearrangement`` (`#258`_):
   This is a bigger discussion involving ComRepo, DataRep and GLDB.
   However, as it does not affect the existence of the ``[vdj]_call``
   fields, which we require for Set 6, it is **not** a MiniStd topic.
*  Inclusion of species information for cell and locus annotation: As
   discussed during the `MiniStd Call 10/2019`_ and decided in
   `MiniStd Call 11/2019`_, we want to introduce fields to provide
   species information for the ``cell_*`` and ``locus`` fields to 
   address issue `#137`_. The respective changes were introduced in PR
   `#260`_, however it turns out that it is problematic to add
   ontology-controlled fields to the ``rearrangement`` object (`#278`_),
   i.e., for ``locus``. Therefore only ``cell_species`` was added to the
   schema, while ``locus_species`` has been reverted (via `#281`_). Will
   follow up with DataRep and ComRepo on potential solutions.
*  Current NCBI submission stats: Pulled from NCBI based on the "AIRR"
   keyword (note that not all submitted studies include this). Results
   in table191201_ are queried via
   ``https://www.ncbi.nlm.nih.gov/nuccore/?term=AIRR%5BKeyword%5D``
   and show TLS record counts aggregated by BioProject ID:

.. _table191201

+-------------+---------+
| BioProject  | records |
+=============+=========+
| PRJNA545339 |      12 |
+-------------+---------+
| PRJNA336331 |       1 |
+-------------+---------+
| PRJNA488042 |      20 |
+-------------+---------+
| PRJNA520929 |      62 |
+-------------+---------+
| PRJNA338795 |      93 |
+-------------+---------+


New topics
==========

*  Define ``cell`` and ``receptor`` objects: The ongoing work to create
   API endpoints to access single-cell data (`#211`_) has sparked some
   discussion about the ``cell`` and ``receptor`` entities and their
   respective (potential) IDs ``cell_id`` and ``pair_id`` (see lengthy
   discussion in `#273`_). We agree that it would be important to
   include a representation of these objects in the schema and adapt the
   API endpoints accordingly. Will follow up in `MiniStd Call 01/2020`_.


====================
MiniStd Call 01/2020
====================

------
Agenda
------

Decisions
=========

*  Human Population Genetics XT (`#264`_, `#265`_)


Follow-up
=========

*  DataRep decision on ``organism`` field
*  DataRep is now the owner MiAIRR Set 6 fields
*  Object definition for ``receptor`` and ``cell`` (see
   `Christian's comment of 2019-12-24`_ on `#273`_)
*  List of To-Does for MiAIRR v2 (`#305`_)


New Topics
==========

*  Should fields be non-nullable based on the availability of the
   information to the primary data depository (current situation) or the
   necessity of the information for meaningful interpretation? Note that
   the current situation can make it hard for third-party annotators
   (`#310`_).

   *  A few things that non-nullable status could indicate:

      *  Criticality to MiAIRR as a Standard: Fields which one MUST
         always have, as decided by the AIRR Community.
      *  Field one always is expected to have: Not necessarily critical
         to MiAIRR, but hard to understand how one could do a study and
         not have it...
   *  Noted that many of the non-nullable fields are controlled
      vocabularies with ``NULL`` like options such as
      ``library_generation_method``:``other`` and ``physical_linkage``:
      ``none``. Perhaps for non-nullable fields this should be the norm.
      We should consider carefully those fields that have limited
      possible values (booleans, controlled vocabularies lacking
      ``NULL``-like terms) and ensure that if they do not exist, we
      really want that data be not AIRR-compliant.
*  Should we switch notes from Google Docs to Github?
*  Review `CEDAR Templates`_


-------
Minutes
-------

Meta
====

* Date: Fri, 2020-01-17 14:30 UTC
* Present: Brian, Christian, Francisco, John, Sri


Decisions
=========

*  **Approved** Human Population Genetics XT (`#264`_, `#265`_)
*  **Approved** moving/introducing the fields ``ancestry_population``,
   ``country_birth`` and ``collection_country`` to/in an Extension.
*  As ``ethnicity`` and ``race`` have neither a consistent scientific
   concept nor globally applicable ontologies, they are **removed** from
   MiAIRR and its extensions. Note that annotators who wish to provide
   this information can still do so using these keywords as ``optional``
   free text fields.
*  The integration of extensions into the schema still needs to be
   discussed with DataRep. Therefore a first draft has now been commited
   (`#318`_).


Follow-up
=========

*  DataRep deferred the decision on whether to rename ``organism`` to
   ``species``, will bring it up again in `MiniStd Call 02/2020`_.
*  DataRep has acknowledged that they are now the owner of the fields
   in Set 6 (see minutes of `MiniStd Call 11/2019`_ and
   `MiniStd Call 12/2019`_)
*  We are now collecting things that need to be included for MiAIRR v2
   in `#305`_. In most cases the things will/should also have an entry
   of their own on the issue tracker, in which case these should be
   labeled with the ``AIRRv2.0`` and the ``MiAIRR`` tag in addition.
*  ``cell`` and ``receptor`` objects (`#273`_, `#211`_, `#206`_): There
   is now an emerging consensus based on
   `Christian's comment of 2019-12-24`_ on `#273`_. This has been
   approved by DataRep, Sri is now working on a schema definition. Note
   that ``pair_id`` never made it into an official release, thus it is
   simple to deprecate it.


New Topics
==========

*  Revisit MiAIRR non-nullable fields (`#310`_): Currently non-nullable
   status (aka ``required``) is based on the near-certain availability
   of the information to the primary data depository. However, it turns
   out that this makes it hard for third-party annotators, therefore it
   has been proposed to revisit these fields based on the criterium
   whether the information is strictly required for meaningful
   interpretation of the annotated data.
*  John will soon make the CEDAR AIRR templates publicly available and
   asks for comments (link to `CEDAR Templates`_). Note that these
   templates are identical to the information on the actual CEDAR
   submission site, it is just accessible without requiring a login. In
   case you would like to comment on this, please get in contact with
   John until Thu, 2020-01-23.
*  Discussed whether it would be worthwhile to put the agendas and
   minutes on Github instead of GDocs. This would resolve some of the
   overhead that the current workflow produces. Brian comments that
   ComRepo has experimented with this, but not adapted a Github workflow
   as copyediting can be an issue as documents will be public. Will
   discuss again in the next call.


====================
MiniStd Call 02/2020
====================

------
Agenda
------

Follow-up
=========

*  Object definition for ``receptor`` and ``cell`` (in `#320`_, also
   see `Christian's comment of 2019-12-24`_ in `#273`_)
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

*  DataRep deferred the decision on renaming ``organism`` to ``species``
   again, will bring it up again in `MiniStd Call 03/2020`_.
*  Object definition ``cell`` and related data schema: Discussed at
   ComRepo call, Sri will go ahead with a schema and API implementation
   that initially will **not** support a tabular serialization (as it
   requires quite some nesting). Information on data schema can be found
   in `Sri's comment of 2020-02-26`_.
*  `CEDAR Templates`_: Confirmed that templates and their elements can
   be publicly visible (not requiring login). Also confirmed that
   CEDAR's version number can be distinct from MiAIRR version (assuming
   that it clearly labeled).
*  Switching to Github for agendas and minutes: Again no objections,
   starting test run for this call.


MiAIRR requirement levels
=========================

*  This is a combination of issues `#310`_ and `#297`_, which deal with
   nullable status of field, how to indicate this to users and how to
   represent it in the data schema.
*  We currently have three requirement levels (adopted from RFC2119)
   in table200201_, where:

   *  "present" means that a field exists in a metadata description
   *  "NULL" means that a field has a ``NULL`` value (as in SQL) or a
      ``NULL``-like value that does also not provide any information on
      regarding this field. ``NULL``-like values are currently
      ``missing``, ``not applicable`` and ``not collected``, which were
      adopted from `BioSample attributes`_
   *  MiAIRR field are by default ``recommended`` as they are part of
      a minimal standard and thus MUST be present. Some MiAIRR fields
      might be ``required`` but never ``optional``

.. _table200201:

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

*  ``read_length`` field

   *  Moved ``*read_length`` to Set 4 in `#324`_, merged.
   *  Strictly spoken, the addition of the other ``set: 4`` fields
      already broke compatibility as they are new requirements that were
      not present in AIRRv1.0. However ``set: 4`` is a dark place for
      MiAIRR anyhow, as it is just defined as raw data (i.e., not
      mandatory metadata, so in the real world nothing depends on this).
   *  NCBI mapping needs to be updated, documented in `#330`_
   *  Format change is could be relevant to CEDAR, who have noted this.
   *  Topic can be closed, no follow-up in March until issues arise.


====================
MiniStd Call 03/2020
====================

------
Agenda
------

Follow-up
=========

*  DataRep has decided to rename ``organism`` to ``species``. Their
   change will likely go into v1.3 and therefore predate our change,
   which is slated for v2.0. DataRep will also discuss how to annotate
   the renaming (`#248`_).
*  Object definition ``cell`` and related data schema: Schema is now
   in branch XXX. We however need to discuss about:

   *  "True" ``Repertoires`` and "Meta"-``Repertoires`` (the former ones
      contain each cell object only once, the latter ones can contain
      them multiple time (either copied or linked).
   *  If a ``Rearrangement`` is defined as an *observed nucleic acid*
      how do we represent UMI- and CellID-based collapsing. Is there
      a separate object for it?

*  MiAIRR requirement levels:

   *  There is a general consensus in DataRep and ComRepo to move away
      from the current RFC2119 terms, as they can create confusion with
      the OpenAPI ``required`` term.
   *  A current suggestion are the RDA-inspired terms ``essential``,
      ``important`` and ``useful`` (see `#342`_).
   *  John noted that we need to distinguish between terms for
      individual fields and qualification of the whole metadata record
      for a given use case. Therefore, for most fields the requirement
      levels could be differ between use cases. Therefore he suggests
      that there are mainly two options that would potentially work:

      1. Use a binary criterium (e.g. ``MiAIRR compliant``), which
         applies if and only if all required fields are provided. The
         non-nullable requirement could be relabeled as a question of
         the ontology/vocabulary for the field.
      2. Spell out the individual requirement for each use case (or
         group of use cases).

*  Switch to Github for agendas and minutes: First round of feedback.


New Topics
==========

*  Merger of AIRR Standards WG: ComRepo, DataRep and MiniStd currently
   have 4--5 calls every month in which a core group of 5--6 people
   frequently talk about similar topics to an extended group of
   participants. We would like to see whether we can increase the
   efficiency of this process by having one joint meeting per month,
   covering the topics of MiniStd and DataRep and the API parts of
   ComRepo. In addition the original WG can have additional calls
   between the general calls (maybe with a fixed schedule and cancel
   if not necessary). If this works out and lead to more fun, less
   meetings and/or increased productivity, we would propose an
   official merger of the WGs at the next AIRR-C meeting.


.. ======================================================================
.. == Unlisted Links to AIRR Standards Github issues and pull requests ==
.. ======================================================================

.. _`#137`: https://github.com/airr-community/airr-standards/issues/137
.. _`#192`: https://github.com/airr-community/airr-standards/issues/192
.. _`#206`: https://github.com/airr-community/airr-standards/issues/206
.. _`#211`: https://github.com/airr-community/airr-standards/issues/211
.. _`#248`: https://github.com/airr-community/airr-standards/issues/248
.. _`#258`: https://github.com/airr-community/airr-standards/issues/258
.. _`#260`: https://github.com/airr-community/airr-standards/pull/260
.. _`#264`: https://github.com/airr-community/airr-standards/issues/264
.. _`#265`: https://github.com/airr-community/airr-standards/issues/265
.. _`#266`: https://github.com/airr-community/airr-standards/issues/266
.. _`#273`: https://github.com/airr-community/airr-standards/issues/273
.. _`#278`: https://github.com/airr-community/airr-standards/issues/278
.. _`#279`: https://github.com/airr-community/airr-standards/issues/279
.. _`#281`: https://github.com/airr-community/airr-standards/pull/281
.. _`#297`: https://github.com/airr-community/airr-standards/issues/297
.. _`#305`: https://github.com/airr-community/airr-standards/issues/305
.. _`#308`: https://github.com/airr-community/airr-standards/issues/308
.. _`#310`: https://github.com/airr-community/airr-standards/issues/310
.. _`#318`: https://github.com/airr-community/airr-standards/pull/318
.. _`#319`: https://github.com/airr-community/airr-standards/pull/319
.. _`#320`: https://github.com/airr-community/airr-standards/issues/320
.. _`#324`: https://github.com/airr-community/airr-standards/pull/324
.. _`#328`: https://github.com/airr-community/airr-standards/issues/328
.. _`#330`: https://github.com/airr-community/airr-standards/issues/330
.. _`#342`: https://github.com/airr-community/airr-standards/issues/342


.. _`Christian's comment of 2019-12-24`: https://github.com/airr-community/airr-standards/issues/273#issuecomment-568649516
.. _`Sri's comment of 2020-02-26`_:    https://github.com/airr-community/airr-standards/issues/320#issuecomment-591416785

.. == Other Unlisted Links ==
.. _`CEDAR Templates`: https://openview.metadatacenter.org/templates/https:%2F%2Frepo.metadatacenter.org%2Ftemplates%2Fea716306-5263-4f7a-9155-b7958f566933
.. _`INSDC Feature Table`: http://www.insdc.org/documents/feature-table
.. _`BioSample attributes`: https://www.ncbi.nlm.nih.gov/biosample/docs/attributes/
