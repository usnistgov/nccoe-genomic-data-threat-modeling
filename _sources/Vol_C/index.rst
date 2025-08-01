Genomic Data Threat Modeling: Privacy 
=====================================

An Implementation for Genomic Data Sequencing and Analysis
-----------------------------------------------------------

.. include:: /_publication_note.rst

+--------------------+--------------------------+--------------------+-----------------------------+
| **Ron Pulivarti**  | **Brett Kreider**        | **Scott Ross**     | **Isabelle Brown-Cantrell** |
|                    |                          |                    |                             |
| **Justin Wagner**  | **Stuart S. Shapiro**    | **Philip Whitlow** | **Patrick Pape**            |
|                    |                          |                    |                             |
| National Institute | **Julie Nethery Snyder** | HudsonAlpha        | **Jared Sheldon**           |
|                    |                          |                    |                             |
| of Standards and   | **Kevin E. Wilson**      |                    | The University of           |
|                    |                          |                    |                             |
| Technology         | **Martin Wojtyniak**     |                    | Alabama in Huntsville       |
|                    |                          |                    |                             |
|                    | MITRE Corporation        |                    |                             |
+--------------------+--------------------------+--------------------+-----------------------------+

.. image:: media/Logos.png
   :alt: This graphic contains the logos for NIST and the NCCoE.

INITIAL PUBLIC DRAFT

**DISCLAIMER**

Certain commercial entities, equipment, products, or materials may be identified by name or company logo or other insignia in order to acknowledge their participation in this collaboration or to describe an experimental procedure or concept adequately. Such identification is not intended to imply special status or relationship with NIST or recommendation or endorsement by NIST or NCCoE; neither is it intended to imply that the entities, equipment, products, or materials are necessarily the best available for the purpose.

National Institute of Standards and Technology Special Publication 1800-43, Natl. Inst. Stand. Technol. Spec. Publ. 1800-43, 55 pages, (August 2025), CODEN: NSPUE2

**NIST Technical Series Policies**
Copyright, Use, and Licensing Statements `NIST Tech Pubs Policy <https://doi.org/10.6028/NIST-TECHPUBS.CROSSMARK-POLICY>`__
NIST Technical Series Publication Identifier Syntax `NIST Tech Pubs IDs <https://www.nist.gov/nist-research-library/nist-technical-series-publications-author-instructions#pubid>`__

**Author ORCID iDs**

-  Ronald Pulivarti: 0000-0002-8330-3474

-  Justin Wagner: 0009-0003-8903-0504

-  Brett Kreider: 0009-0004-1508-5876

-  Stuart Shapiro: 0000-0003-3676-7388

-  Julie Nethery Snyder: 0009-0004-6352-2831

-  Kevin Wilson: 0009-0008-3673-6040

-  Martin Wojtyniak: 0009-0005-9643-2194

-  Scott Ross: 0009-0002-8672-6496

-  Philip Whitlow: 0009-0000-7677-3825

-  Isabelle Brown-Cantrell: 0009-0004-8820-6448

-  Patrick Pape: 0009-0005-4922-4026

-  Jared Sheldon: 0009-0009-7909-4217

**FEEDBACK**
You can view or download the draft guide at the `NCCoE Genomics Project Page <https://www.nccoe.nist.gov/projects/cybersecurity-and-privacy-genomic-data>`. 

Comments on this publication may be submitted to: genomic_cybersecurity_nccoe@nist.gov.

All comments are subject to release under the Freedom of Information Act. NIST welcomes feedback and input on any aspect of this document and additionally proposes a list of non-exhaustive questions and topics for consideration: 

   1.	How well does the threat modeling exercise in this guide relate to existing efforts in your organization? Are there significant gaps between the sets of practices that this guide should address? 
   2.	How do you expect this document to influence your future practices and processes? 
   3.	What changes would you like to see to increase or improve your organization’s use of this document? 
   4.	What suggestions do you have on changing the format of the information provided?  
   5.	Is the example provided here sufficient for your organization to identify and address genomic data threats in sequencing or data analysis? Are there changes or additional content that the authors should consider? 

| National Cybersecurity Center of Excellence
| National Institute of Standards and Technology
| 100 Bureau Drive
| Mailstop 2002
| Gaithersburg, MD 20899
| Email: nccoe@nist.gov

**NATIONAL CYBERSECURITY CENTER OF EXCELLENCE**

The National Cybersecurity Center of Excellence (NCCoE), a part of the National Institute of Standards and Technology (NIST), is a collaborative hub where industry organizations, government agencies, and academic institutions work together to address businesses’ most pressing cybersecurity issues. This public-private partnership enables the creation of practical cybersecurity solutions for specific industries, as well as for broad, cross-sector technology challenges. Through consortia under Cooperative Research and Development Agreements (CRADAs), including technology partners—from Fortune 50 market leaders to smaller companies specializing in information technology security—the NCCoE applies standards and best practices to develop modular, adaptable example cybersecurity solutions using commercially available technology. The NCCoE documents these example solutions in the NIST Special Publication 1800 series, which maps capabilities to the NIST Cybersecurity Framework and details the steps needed for another entity to re-create the example solution. The NCCoE was established in 2012 by NIST in partnership with the State of Maryland and Montgomery County, Maryland.

To learn more about the NCCoE, visit https://www.nccoe.nist.gov/. To learn more about NIST, visit https://www.nist.gov.

**NIST Cybersecurity Practice Guides**
NIST Cybersecurity Practice Guides (Special Publication 1800 series) target specific cybersecurity challenges in the public and private sectors. They are practical, user-friendly guides that facilitate the adoption of standards-based approaches to cybersecurity. They show members of the information security community how to implement example solutions that help them align with relevant standards and best practices, and provide users with the materials lists, configuration files, and other information they need to implement a similar approach.

The documents in this series describe example implementations of cybersecurity practices that businesses and other organizations may voluntarily adopt. These documents do not describe regulations or mandatory practices, nor do they carry statutory authority.

**ABSTRACT**

This paper provides an example of how to conduct genomic data threat modeling for privacy on a data processing environment, including documenting the architecture, identifying threats, applying sample interventions, and iterating the process as needed. The paper complements the earlier NIST CSWP 35, Cybersecurity Threat Modeling the Genomic Data Sequencing Workflow. 

**KEYWORDS**

Genomic privacy; genomic data threat modeling; Privacy Framework; DNA sequencing; genomics; genomic data; genomic sequencing; human genome; threat interventions.

**ACKNOWLEDGMENTS**

The authors would like to thank Dylan Gilbert, former Privacy Policy Advisor, NIST Privacy Engineering Program; Justin Zook, NIST Material Measurement Laboratory; and Meagan Cochran, HudsonAlpha Institute for Biotechnology; Cherilyn Pascoe, NIST/NCCoE; Diane Wertime, NIST; Gary Howarth, NIST; Hannah Zook, NIST; Sue Wang, NCCoE; Drew Keller, NCCoE.

**DOCUMENT CONVENTIONS**

The terms “shall” and “shall not” indicate requirements to be followed strictly to conform to the publication and from which no deviation is permitted. The terms “should” and “should not” indicate that among several possibilities, one is recommended as particularly suitable without mentioning or excluding others, or that a certain course of action is preferred but not necessarily required, or that (in the negative form) a certain possibility or course of action is discouraged but not prohibited. The terms “may” and “need not” indicate a course of action permissible within the limits of the publication. The terms “can” and “cannot” indicate a possibility and capability, whether material, physical, or causal.

**CALL FOR PATENT CLAIMS**

This public review includes a call for information on essential patent claims (claims whose use would be required for compliance with the guidance or requirements in this Information Technol-ogy Laboratory (ITL) draft publication). Such guidance and/or requirements may be directly stated in this ITL Publication or by reference to another publication. This call also includes disclosure, where known, of the existence of pending U.S. or foreign patent applications relating to this ITL draft publication and of any relevant unexpired U.S. or foreign patents.
ITL may require from the patent holder, or a party authorized to make assurances on its behalf, in written or electronic form, either:
a) assurance in the form of a general disclaimer to the effect that such party does not hold and does not currently intend holding any essential patent claim(s); or
b) assurance that a license to such essential patent claim(s) will be made available to applicants de-siring to utilize the license for the purpose of complying with the guidance or requirements in this ITL draft publication either:
1.	under reasonable terms and conditions that are demonstrably free of any unfair discrimina-tion; or 
2.	without compensation and under reasonable terms and conditions that are demonstrably free of any unfair discrimination. 
Such assurance shall indicate that the patent holder (or third party authorized to make assurances on its behalf) will include in any documents transferring ownership of patents subject to the assur-ance, provisions sufficient to ensure that the commitments in the assurance are binding on the transferee, and that the transferee will similarly include appropriate provisions in the event of fu-ture transfers with the goal of binding each successor-in-interest. 
The assurance shall also indicate that it is intended to be binding on succes-sors-in-interest regardless of whether such provisions are included in the relevant transfer docu-ments. 
Such statements should be addressed to: genomic_cybersecurity_nccoe@nist.gov


.. toctree::
   :maxdepth: 1
   :titlesonly:
   :glob:
   :hidden:

   Summary <Summary.rst>
   Introduction <Introduction.rst>
   Genomic Data Threat Modeling Example <PTM/index.rst>
   Conclusion <Conclusion.rst>
   Appendices <Appendix/index.rst>

 



 











 