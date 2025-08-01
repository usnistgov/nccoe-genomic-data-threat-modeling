Appendices
===========

Appendix A: Abbreviations and Acronyms
--------------------------

The following acronyms are used in this publication.

**ATT&CK**

**Adversarial Tactics, Techniques & Common Knowledge**

**CAP**

College of American Pathologists

**CLIA**

Clinical Laboratory Improvement Amendments

DFD

Dataflow Diagram

**DMZ**

Demilitarized Zone

DNA

Deoxyribonucleic acid

**FDA**

Food and Drug Administration

**GCP**

Good Clinical Practice

**GDPR**

EU General Data Protection Regulation

**GINA**

Genetic Information Nondiscrimination Act of 2008

**HIPAA**

Health Insurance Portability and Accountability Act

**IR**

Internal Report

**IRB**

Institutional Review Board

LIMS

Laboratory Information Management System

**LINDDUN**

Linking, Identifying, Detecting, Data Disclosure, Unawareness and Unintervenability, and Non-compliance privacy threat types

MO

Mission Objective

NCCoE

National Cybersecurity Center of Excellence

NIH

National Institutes of Health

NIST

National Institute of Standards and Technology

OSS

Open-Source Software

**PANOPTIC**

Pattern and Action Nomenclature Of Privacy Threats In Context

**PEO**

Privacy Engineering Objective

**PET**

Privacy-Enhancing Technology

**PF**

NIST Privacy Framework

**PRAM**

Privacy Risk Assessment Methodology

SP

NIST Special Publication

STRIDE

Spoofing, Tampering, Repudiation, Information Disclosure, and Elevation of Privilege cybersecurity threat types

**SQL**

Structured Query Language

**TRF**

Test Request Form

Threat Modeling Approach
========================

As some genomic sequencers are classified as medical devices, the cybersecurity paper used the threat modeling approach described in the *Playbook for Threat Modeling Medical Devices (Playbook)* *[18]* based on methods described in the “Threat Modeling Manifesto” *[19]* and by Shostack *[17]*. However, as noted above, privacy, though connected to cybersecurity, is distinct from it. Therefore, while this paper adheres to the high-level approaches of the Four Question Framework and the Threat Modeling Manifesto, it employs tools that are specific to privacy.

.. image:: media/Appendix-Figure1.gif
   :width: 4.75917in
   :height: 3.19464in

   Figure 4. Visualization of the Four Question Framework for Threat Modeling *[17]*

This figure illustrates The Four Questions Framework for Threat Modeling. It starts with Question 1: What are we working on? From there, Question 2 is What could go wrong? Question 3 is What are we going to do about it? And Question 4 is Did we do a good job? The questions interconnect and will be revisited iteratively to improve the results.|\ |This figure illustrates The Four Questions Framework for Threat Modeling. It starts with Question 1: What are we working on? From there, Question 2 is What could go wrong? Question 3 is What are we going to do about it? And Question 4 is Did we do a good job? The questions interconnect and will be revisited iteratively to improve the results.

It is expected that users of this process aiming to leverage the outputs documented in this paper will modify and adjust them to reflect differences between their environments and the baseline one described here. In particular, this threat model is intended for various stakeholders who have differing priorities with respect to the same threats. Organizations will choose specific responses, including interventions, depending on:

- their mission;

- their goals in performing the threat modeling process;

- the priorities that reflect their specific use case;

- the phase of the system life cycle; and

- the resources at their disposal.

Therefore, a comprehensive list of interventions and answers to Question 3 will not be provided in this paper. `Section 4.2 <#_Response_Determination>`__ discusses the intervention identification process along with resources and an illustrative example. Individual organizations can also incorporate the threats into their risk modeling and assessment processes, addressing the resultant risks through elimination, mitigation, transfer, or acceptance.

Privacy Threat Modeling
-----------------------

Key characteristics of privacy threats are a superset of the characteristics of cybersecurity threats. Cybersecurity threats typically involve the actions of a malicious entity that is external to the system proper. This can be true of privacy threats as well, but not necessarily. While privacy threats can be active, they can also involve inactions, such as a failure to provide relevant information to direct data subjects or to obtain their consent for the collection and use of their data. Malicious privacy threats are certainly not unheard of, but privacy threats are just as often side effects of the pursuit of other objectives. Additionally, while threat actors can be external entities, sometimes it is the system itself, operating as designed, that poses the threat. One such privacy threat is insufficient de-identification, where the identity of an individual in a sensitive dataset, such as a rare disease database, can be determined using metadata and information from open-access or controlled-access genomic databases *[15]*.

As a result of these possibilities, privacy threat modeling must adopt a broader perspective than cybersecurity threat modeling. This broader perspective is reflected in the principal tools employed – the NIST PRAM *[1]*, LINDDUN *[2]*, and MITRE PANOPTIC™ *[3]*– each of which are described in the following subsections. Two of those tools, LINDDUN and PANOPTIC, were also selected because they roughly mirror the orientations of the tools – STRIDE *[16]* and MITRE ATT&CK® *[17]* respectively – that were used for the cybersecurity threat modeling in NIST CSWP 35 *[6]*.

LINDDUN
~~~~~~~

LINDDUN *[2]* is one of the earliest and most widely recognized privacy threat modeling tools. Inspired by STRIDE *[12]*, the name is an acronym comprising seven different privacy threat types:

- Linking – Learning more about an individual (*or a group*) by associating related data items with one another

- Identifying – Identity of an individual can be learned through leaks, deduced, or inferred when that is undesirable

- Non-repudiation [1]_ – An individual is unable to deny certain claims pertaining to them as a result of data collected, data shared, or a system action taken by the individual or others

- Detecting – Becoming aware of an individual’s involvement, membership, or participation via observation of relevant information

- Data disclosure – Avoidable transfer of an individual’s data across a boundary, whether intended or unintended

- Unawareness and unintervenability – Insufficiently informing, involving, or empowering the individual with respect to their role and relation to the system

- Non-compliance – Lack of adherence to statutory or regulatory requirements or to standards or best practices

LINDDUN *[2]* heavily relies on DFDs, which are especially useful for data privacy analyses. Like STRIDE-per-Element *[12]*, DFD elements vary in their relevance for different threat types. LINDDUN comes with a catalog of detailed threat trees that break down the high-level threat types into more granular threats that can be associated with specific DFD segments *[2]*.

MITRE PANOPTIC™
~~~~~~~~~~~~~~~

Just as LINDDUN *[2]* roughly mirrors STRIDE *[16]*, PANOPTIC *[3]* roughly mirrors MITRE ATT&CK *[17]*. Like ATT&CK, PANOPTIC (Pattern and Action Nomenclature Of Privacy Threats In Context) was created from the bottom up based on real-world privacy attacks drawn from multiple sources. However, PANOPTIC looks and works rather differently. PANOPTIC consists of two closely related taxonomies: Contextual Domains (made up of contextual elements) and Privacy Activities (made up of privacy threat actions). The Contextual Domains, as the name suggests, capture important contextual aspects of the system of concern, including how it interacts with data subjects and the nature of the data. Privacy Activities describe the various components of a privacy attack and are a mixture of Fair Information Practice Principles, information life cycle stages such as collection and processing, and independent components such as identification. Contextual elements and privacy threat actions may have sub-elements and sub-actions respectively. *Table 23* lists the Contextual Domains and definitions while *Table 24* lists the Privacy Activities and definitions. [2]_

.. table:: Table 23. PANOPTIC V2.0 Contextual Domains

   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **ID** | **Contextual Domain** | **Definition**                                                                                                                                                       |
   +========+=======================+======================================================================================================================================================================+
   | PC01   | Environment           | The type of contextual domain in which data actions [3]_ occur                                                                                                       |
   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PC02   | Distribution          | How many entities with which the information holder shares information                                                                                               |
   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PC03   | Interaction           | The extent to which the data subject or their proxy interacts with the data custodian, processor, third-party, or their proxy (entities other than the data subject) |
   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PC04   | Engagement            | Targeted subpopulations with which the entity or their proxy interact                                                                                                |
   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PC05   | Data Type             | Classes of data upon which data actions are performed                                                                                                                |
   +--------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: Table 24. PANOPTIC V2.0 Privacy Activities

   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | **ID** | **Privacy Activity**    | **Definition**                                                                                            |
   +========+=========================+===========================================================================================================+
   | PA01   | Notice                  | Informing the data subject or their proxy of one or more data actions                                     |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA02   | Consent                 | Assent from the data subject or their proxy to one or more defined data actions                           |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA03   | Collection              | The gathering or extraction of information                                                                |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA04   | Insecurity              | Insufficient data protection controls                                                                     |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA05   | Identification          | How information is associated with the data subject                                                       |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA06   | Quality Assurance       | Implementing policies or processes to ensure quality throughout privacy-related activities                |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA07   | Manageability [4]_      | Enabling the data subject or their proxy to access, modify, copy, or destroy information about themselves |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA08   | Aggregation             | Assembling data from one or more sets of data                                                             |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA09   | Processing              | Extracting and developing value and utility from information                                              |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA10   | Sharing                 | Making information available to another entity                                                            |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA11   | Use                     | Leveraging information to achieve a goal                                                                  |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA12   | Retention & Destruction | Actions that affect the persistence of information                                                        |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+
   | PA13   | Deviations              | Data action diverges from established limits bounding the data action in question                         |
   +--------+-------------------------+-----------------------------------------------------------------------------------------------------------+

NIST Privacy Risk Assessment Methodology (PRAM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The NIST PRAM *[1]* is a product of NIST’s Privacy Engineering Program. It is a multi-step process for identifying system privacy risks and is supported by a set of four worksheets:

1. Framing Business Objectives & Organizational Privacy Governance

2. Assessing System Design (includes separate Supporting Data Map)

3. Prioritizing Risk

4. Selecting Controls

The PRAM also leverages a non-exhaustive privacy risk model consisting of defined “Problematic Data Actions” – particular manifestations of the higher-level data actions corresponding to stages of the information life cycle [5]_, which could enable adverse effects for individuals – and “Problems for Individuals,” those adverse consequences. The PRAM is intended to help ensure systems reflect the PEOs listed in `Section 1.3 <#_Privacy_Overview>`__.

As a risk modeling tool, the PRAM is broader than threat modeling. However, aspects of it can be readily adapted to directly accommodate privacy threat modeling. Therefore, the first two worksheets enumerated above were modified as necessary and used as the principal means of documenting the threat modeling described in this paper.

Organizational Tailoring
------------------------

Organizations that process genomic data need to protect that data due to its high value and the privacy risk to individuals. Organizations need a process to guide the selection of appropriate capabilities to reduce privacy risk to an acceptable level for the predictability, manageability, and disassociability of systems that process genomic data. Each organization should consider its own goals and priorities when tailoring this example to select and implement appropriate and cost-effective privacy capabilities and threat interventions. The organization should also periodically reassess its privacy posture and update its threat modeling as necessary, considering new technologies and threats to identify gaps and reprioritize interventions.

NIST IR 8467, the *Genomic Data Profile* *[4]*\ *,* provides a prioritized list of Mission Objectives (MOs) for organizations processing genomic data and prioritizes NIST Privacy Framework (PF) version 1.0 Subcategories (or outcomes) to support achieving those MOs. Based on the workflow of sequencing genomic material, the NCCoE team selected four relevant MOs from the *Genomic Data Profile* *[4]*, shown in *Table 25.* However, depending on their context, organizations may choose to prioritize an alternative set of MOs.

.. table:: Table 25. Selected Genomic Sequencing Workflow Mission Objectives

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | Mission Objective from the Genomic Data Profile | Mission Objective Description                                                                             |
   +=================================================+===========================================================================================================+
   | 2                                               | Manage privacy risk to existing and future relatives                                                      |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | 3                                               | Identify, model, and address cybersecurity and privacy risks of processing genomic data                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | 5                                               | Manage privacy risk to donors                                                                             |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | 12                                              | Promote the use of privacy-enhancing technologies as well as secure technologies for sharing genomic data |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------+

When answering Question 3 (What are we going to do about it?) of the Four Question Framework these MOs can be used to prioritize potential controls that might be employed to disrupt threats.

Methodology Overview
====================

This appendix summarizes the methodology presented in the body of the paper for easy reference. Note that while this methodology is presented sequentially, it is often iterative in practice.

*Question 1: What are we working on?*

1. Define the target of the threat modeling by identifying system boundaries. Note that the target may constitute a system of systems. Also identify the relevant Mission Objectives from the NIST *Genomic Data Profile.*

2. Identify the different use cases.

3. Complete PRAM Worksheet 1 to capture organizational objectives and privacy governance.

4. Document system context.

   a. In adapted PRAM Worksheet 2, complete System Privacy Capabilities related to the NIST Privacy Engineering Objectives (PEOs) for each use case. Include the security objectives if cybersecurity threat modeling is not being performed separately.

   b. Create a PANOPTIC Contextual Domains mapping for the system using the PANOPTIC mapping template.

   c. Complete Contextual Factors in Worksheet 2, leveraging responses in Worksheet 1 and the PANOPTIC Contextual Domains mapping.

5. Create dataflow diagrams (DFDs) for the different use cases (including a shared DFD if there is a high degree of commonality across the pipelines of the different use cases).

   a. Associate each component with a managing entity and each discrete dataflow with descriptive data actions.

   b. Organize the diagrams using PRAM data actions as swim lanes: collection, generation/transformation, retention/logging, disclosure/transfer, disposal.

   c. Create indices of components and any distinguishing sub-cases and label DFD sources and destinations accordingly.

*Question 2: What could go wrong?*

6.  Using the Assess System Design sheet in Worksheet 2, document each DFD segment – source, flow, destination – including data actions and relevant context. If preferred, use a separate sheet for each DFD.

7.  Identify potential LINDDUN threats for each dataflow segment entry using the LINDDUN threat trees. Ensure that all identified threats are defined from the perspective of the data subject. Create duplicate entries to accommodate multiple threats.

8.  Combine the LINDDUN analyses of the individual DFDs (if applicable) and group the entries by sorting on the LINDDUN threat designation.

9.  Create a PANOPTIC Privacy Activities mapping for each use case using the PANOPTIC mapping template. In doing so, identify relevant or potentially relevant threat actions that could form a privacy attack on one or more data subjects and define scenarios for specific sets of threat actions that could constitute attacks.

10. Validate all threats:

    a. Leveraging the PANOPTIC – LINDDUN mapping, confirm that there is at least one entry in the combined LINDDUN analysis table related to each PANOPTIC attack. Eliminate from further consideration attacks without a corresponding LINDDUN threat. Eliminate from further consideration LINDDUN threats unrelated to any PANOPTIC attack.

    b. For each remaining threat, confirm that it threatens one or more PEO. Eliminate from further consideration any threats that would not undermine at least one PEO.

*Question 3: What are we going to do about it?*

11. Prioritize threats

    a. Assign categorical values for feasibility and difficulty to each validated threat.

    b. Adjust the attack feasibility-difficulty matrix values and/or LINDDUN threat weights if necessary.

    c. Rank order the threats by sorting on computed prioritization values (multiplying the feasibility-difficulty value by the LINDDUN threat weight). List threats from highest to lowest value.

12. Determine threat responses – eliminate, disrupt, transfer, or accept – starting from the highest priority threat and moving down the list.

13. If opting to disrupt a threat:

    a. Identify one or more critical threat actions of the PANOPTIC attack.

    b. Find the NIST Privacy Framework Subcategories associated with each critical threat action. Rank order the Subcategories based on the priorities associated with the selected Mission Objectives in the *Genomic Data Profile.*

    c. In order of Subcategory priority, use the NIST PF – SP 800-53r5 crosswalk to review controls that are relevant for each Subcategory. Select those controls that most directly address the threat action(s).

    d. Note that selected controls are likely to disrupt other, similar attacks.

System Description
==================

PANOPTIC Contextual Mapping for Clinical Use Case
=================================================

.. image:: media/Appendix-Figure2.gif
   :width: 4.66663in
   :height: 8.09198in

PANOPTIC Contextual Mapping for Research Use Case
=================================================

.. image:: media/Appendix-Figure3.gif
   :width: 6.5in
   :height: 4.27847in

Dataflow Diagram Legend 
========================

Table 25. Symbols Used in Detailed DFDs

.. table:: Table 2. Symbols Used in Detailed DFDsData Flow Diagrams (DFDs) created by the team to document their work, showing trust boundaries and communication paths. These diagrams support STRIDE threat analysis and help create a common architecture document for collaboration. They follow conventions

   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Element**     | **Symbol**                                                                                     | **Discussion**                                                                                                                                                                           |
   +=================+================================================================================================+==========================================================================================================================================================================================+
   | External Entity | .. image:: media/Appendix-DFDTable-Icon1.png                                                   | **Object:** A sharp-cornered rectangle.                                                                                                                                                  |
   |                 |                                                                                                |                                                                                                                                                                                          |
   |                 |                                                                                                | **Represents:** Anything outside your control. Examples include people and systems run by other organizations or even divisions.                                                         |
   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process         | .. image:: media/Appendix-DFDTable-Icon2.png                                                   | **Object:** A rounded rectangle.                                                                                                                                                         |
   |                 |                                                                                                |                                                                                                                                                                                          |
   |                 |                                                                                                | **Represents:** Any digital or physical process that generates or manipulates data, including running code, scripts, shell commands, Structured Query Language (SQL) queries, et cetera. |
   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Data Store      | .. image:: media/Appendix-DFDTable-Icon3.png                                                   | **Object:** A drum.                                                                                                                                                                      |
   |                 |                                                                                                |                                                                                                                                                                                          |
   |                 |                                                                                                | **Represents:** Anywhere data are stored, including files, databases, shared memory, cloud storage services, cookies, et cetera.                                                         |
   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Dataflows       | .. image:: media/Appendix-DFDTable-Icon4.png                                                   | **Object:** A double-headed arrow.                                                                                                                                                       |
   |                 |                                                                                                |                                                                                                                                                                                          |
   |                 |                                                                                                | **Represents:** All the ways that components can exchange data with one another. If a flow is unidirectional, you can represent the sending side as an empty arrow.                      |
   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Human Actor     | .. image:: media/Appendix-DFDTable-Icon5.png                                                   | **Object:** A stick figure.                                                                                                                                                              |
   |                 |                                                                                                |                                                                                                                                                                                          |
   |                 |                                                                                                | **Represents:** Any human actor in the environment.                                                                                                                                      |
   +-----------------+------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Each two-dimensional object with solid lines represents a **component**. All lines connecting components represent **dataflows** that can be either digital or physical (such as a network connection or a human inserting a physical sample into a sequencer). Dataflows are shown as double-headed arrows. A **hollow arrow** on one side of a given dataflow implies that the component on that side of the dataflow is the exclusive source.

Dataflow Diagram for Clinical Use Case
======================================

.. image:: media/Appendix-Figure4.gif
   :width: 4.98098in
   :height: 8.61173in


Dataflow Diagram for Research Physical Use Case
===============================================

.. figure:: media/Appendix-Figure5.gif
   :width: 6.5in
   :height: 4.27847in

Dataflow Diagram for Research Digital Use Case
==============================================

.. figure:: media/Appendix-Figure6.gif
   :width: 6.5in
   :height: 4.27847in

Shared Dataflow Diagram
=======================

.. figure:: media/Appendix-Figure7.gif
   :width: 6.5in
   :height: 4.27847in

Dataflow Analysis
=================

Dataflow Analysis for Clinical Use Case
=======================================

.. figure:: media/Appendix-Figure8.gif
   :width: 6.5in
   :height: 4.27847in

Dataflow Analysis for Research Use Case
=======================================

.. figure:: media/Appendix-Figure9.gif
   :width: 6.5in
   :height: 4.27847in

Shared Dataflow Analysis
========================

.. figure:: media/Appendix-Figure10.gif
   :width: 6.5in
   :height: 4.27847in

Integrated and Sorted Dataflow Analysis
=======================================

.. image:: media/Appendix-Figure11.gif
   :width: 8.49408in
   :height: 6.13639in

|.. image:: media/Appendix-Figure12.gif| \ |.. image:: media/Appendix-Figure13.gif|

PANOPTIC Privacy Activities Mapping for Clinical Use Case
=========================================================

|.. image:: media/Appendix-Figure14.gif| \ |.. image:: media/Appendix-Figure15.gif|

PANOPTIC Privacy Activities Mapping for Research Use Case
=========================================================

|.. image:: media/Appendix-Figure16.gif| \ |.. image:: media/Appendix-Figure17.gif|

Scenarios
=========

.. image:: media/Appendix-Figure18.gif
   :width: 4.01988in
   :height: 7.92687in

Threat Validation and Prioritization
====================================

PANOPTIC – LINDDUN Mapping
==========================

.. image:: media/Appendix-Figure19.gif
   :width: 4.26834in
   :height: 8.0159in

Threat Validations and Ranking Attributes
=========================================

.. image:: media/Appendix-Figure20.gif
   :width: 6.5in
   :height: 8.33542in

.. image:: media/Appendix-Figure21.gif
   :width: 6.5in
   :height: 8.60903in

.. image:: media/Appendix-Figure22.gif
   :width: 6.5in
   :height: 8.61667in

.. image:: media/Appendix-Figure23.gif
   :width: 6.5in
   :height: 1.88194in

Ranked Threats
==============

.. image:: media/Appendix-Figure24.gif
   :width: 6.5in
   :height: 8.60347in

.. image:: media/Appendix-Figure25.gif
   :width: 6.5in
   :height: 6.08681in

.. [1]
   Note that this directly conflicts with the repudiation threat type in STRIDE.

.. [2]
   The complete taxonomy with definitions and supporting resources is available at https://ptmworkshop.gitlab.io/#/panoptic.

.. [3]
   Data actions describe broad types of system operations on data such as collection and transformation.

.. [4]
   The PANOPTIC Privacy Activity is distinct from the NIST privacy engineering objective of the same name.

.. [5]
   The NIST Privacy Framework *[15]* defines data processing as the collective set of data actions (i.e., the complete data life cycle, including, but not limited to collection, retention, logging, generation, transformation, use, disclosure, sharing, transmission, and disposal).


.. .. |A rectangle, representing an external entity| image:: media/image4.png
..    :width: 1.1875in
..    :height: 0.77422in
.. .. |A rounded rectangle, representing a process| image:: media/image5.png
..    :width: 1.22222in
..    :height: 0.79828in
.. .. |A cylinder or drum, representing a data store| image:: media/image6.png
..    :width: 1.09722in
..    :height: 0.71536in
.. .. |Two bidirectional arrows, representing data flows. One arrow has the right side tip unfilled| image:: media/image7.png
..    :width: 1.19788in
..    :height: 0.82892in
.. .. |Diagram AI-generated content may be incorrect.| image:: media/image8.png
..    :width: 0.61559in
..    :height: 0.75497in
.. .. |image3| image:: media/image9.emf
..    :width: 9.28631in
..    :height: 4.54212in
.. .. |image4| image:: media/image10.emf
..    :width: 9.27819in
..    :height: 3.7707in
.. .. |image5| image:: media/image11.emf
..    :width: 9.28732in
..    :height: 3.76222in
.. .. |image6| image:: media/image12.emf
..    :width: 9in
..    :height: 4.20208in
.. .. |image7| image:: media/image13.emf
..    :width: 8.79955in
..    :height: 5.66053in
.. .. |image8| image:: media/image14.emf
..    :width: 9in
..    :height: 2.73611in
.. .. |image9| image:: media/image15.emf
..    :width: 9in
..    :height: 2.7625in
.. .. |image10| image:: media/image16.emf

.. .. |image11| image:: media/image17.emf
..    :width: 8.63958in
..    :height: 6.48611in
.. .. |image12| image:: media/image18.emf
..    :width: 9in
..    :height: 4.11111in
.. .. |image13| image:: media/image19.emf
..    :width: 3.43596in
..    :height: 6.13846in
.. .. |image14| image:: media/image20.emf
..    :width: 3.40913in
..    :height: 6.14341in
.. .. |image15| image:: media/image21.emf
..    :width: 3.51804in
..    :height: 6.14178in
.. .. |image16| image:: media/image22.emf
..    :width: 3.49214in
..    :height: 6.20794in

