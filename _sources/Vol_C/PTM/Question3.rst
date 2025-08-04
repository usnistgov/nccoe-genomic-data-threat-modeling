Question 3: "What are we going to do about it?"
===============================================

Once threats have been validated, decisions must be made regarding how to respond. The high-level options for addressing validated threats align with the options for risk management:

1. **Eliminate.** This is the most desired outcome; however, it is often challenging and may involve forgoing a specific feature or functionality. For example, in the case of attack number 1 in the core example (Table 15), removing the receiving clerk from the pipeline by sending physical samples directly to the relevant lab technician would introduce logistical complications that could prove infeasible. If a feature or function is required to accomplish one of the use case’s Mission Objectives (MOs), then eliminating the threat is not possible.

2. **Disrupt.** This involves identifying, adding, and/or improving controls to frustrate attacks. For example, the nexus of attack number 1 in the core example is single source profiling. Controls targeting this threat action would disrupt the entire attack. This is explored in more detail in `Response Determination <Question3.html#response-determination>`__.

3. **Transfer Responsibility.** This strategy transfers responsibility for addressing the threat to another entity, who may have resources of their own to intervene or who can better tolerate the presence of the threat. Documentation of this responsibility transfer and appropriate agreements are an important aspect for implementing this option.

4. **Accept.** In any system, there are threats which are challenging or impossible to disrupt but whose presence is judged to be tolerable. For example, attack number 55 in the core example reflects potential issues of software supply chains. However, the system design may be judged sufficiently robust to warrant accepting the threat of using externally developed software, which may then be paired with threat intelligence monitoring. These accepted threats need to be documented and periodically reviewed, tolerance for accepting threats may change over time. 

When working on Question 3, it is important to consider all four options: eliminate, disrupt, transfer, accept. The impact on the mission posed by the threat, as well as the organization’s threat (and risk) tolerance, will guide decision-making. The most common and perhaps most complex response is to disrupt the threat by applying additional controls or reconfiguring existing ones. There may be multiple interventions (potentially ranging across eliminate, disrupt, and transfer) for a threat with varying costs and effectiveness. Choices should be guided by the organization’s mission, tolerances, and resources. 

If interventions (i.e., responses other than accept), are chosen, they need to be adequately documented to be implementable. There should be sufficient detail to support implementation and testing. If a threat is accepted, the reasoning and assumptions should be documented. In all cases, decisions should be periodically revisited as both the environment and the organization’s risk tolerance may change over time.

This section describes the process of determining threat responses, using the core example as an illustration. In selecting and implementing interventions it is important to consider responsibility, verifiability (preferably automated), maintainability, and usability. All systems will inevitably need updates and modifications; the managing party for verification and maintenance of each intervention needs to be clearly defined.

Threat Prioritization
---------------------

While a small number of threats can be easily prioritized by inspection, typical analyses require a more systematic approach. Therefore, each attack was characterized in terms of its feasibility and difficulty. In this exercise the core example only exhibits a handful of validated threats though the complete example identifies close to 100 as described in Appendix E, G and F with many falling below a prioritization threshold. 

Assigning values to attack feasibility (how credible it is) and difficulty (how hard it is to execute) is inherently subjective. Feasibility reflects a number of factors, including threat actor opportunity, capability, and (in the case of people and organizations) motivation. It is assessed using one of three designations: plausible, implausible, or indeterminate. In those cases where the system itself is the threat actor and the attack is intrinsic to normal system operation, of course, the attack is not only feasible but pre-determined and therefore plausible by definition. Attack difficulty reflects the capabilities and resources required, as well as how many discrete threat actions are involved, and is indicated using a five-step scale. The difficulty scale and context-specific criteria based on the state of the data are given in Table 16.

.. table:: Table 16. Attack Difficulty Scale

   +----------------------+-----------------------------------------------------------------------------------------------+
   | **Difficulty Level** | **Context-specific Data Criteria**                                                            |
   +======================+===============================================================================================+
   | Negligible           | Analyzed results with additional input, professional recommendations, patient PHI             |
   +----------------------+-----------------------------------------------------------------------------------------------+
   | Minor                | Tool output, clinical reports without additional analysis                                     |
   +----------------------+-----------------------------------------------------------------------------------------------+
   | Moderate             | Physical samples or raw sequencing data                                                       |
   +----------------------+-----------------------------------------------------------------------------------------------+
   | Significant          | Metadata produced by the sequencing service devices or sample requests that are pseudonymized |
   +----------------------+-----------------------------------------------------------------------------------------------+
   | Severe               | Information about the machines and analysis tools used or the staff that works there          |
   +----------------------+-----------------------------------------------------------------------------------------------+

Returning to attack number 14, this is a plausible attack based on the necessity of the dataflow through an honest but potentially curious threat actor, the receiving clerk. The attack is of moderate difficulty since it revolves around physical samples and requires knowledge and correlation of certain information. Table 17 shows the characterization for the entire core example. Table 13 lists descriptions of individual PANOPTIC threat actions. 

.. table:: Table 17. Core Example Threat Characteristics

   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | **No.** | **PANOPTIC Attack**                                  | **LINDDUN Threat** | **LINDDUN Analysis**                                                                                                                                                                                                        | **Feasibility** | **Difficulty** |
   +=========+======================================================+====================+=============================================================================================================================================================================================================================+=================+================+
   | 1       | PA03.09, PA03.11, PA08.02.01, PA10.01, PA11.01       | L.2.1.2            | Sending the group of X samples together to the freezers around the same time as a project known to be doing Y disease research could link the samples to Y disease                                                          | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 2       | PA03.09, PA05.02.02, PA08.02.02, PA10.01, PA11.01    | L.2.1.2            | Samples that are put into the LIMS around the same time could receive IDs with linkable characteristics, which then allows linkage of the sample group to a study around the same time, unless the LIMS is cautious of this | Plausible       | Significant    |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 3       | PA03.09, PA05.02.02, PA08.02.02, PA10.01, PA11.01    | L.2.1.2            | Samples that are put into the cluster filesystem around the same time could be interpreted as being linked to a study about Y disease around the same time                                                                  | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 4       | PA03.09, PA05.02.02, PA08.02.02, PA10.01, PA11.01    | L.2.1.2            | Samples sent to the compute nodes around the same time could be interpreted as being linked to a study about Y disease around the same time                                                                                 | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 5       | PA03.09, PA05.02.02, PA08.02.02, PA10.01, PA11.01    | L.2.1.2            | Samples that are put into the data delivery DMZ around the same time could be interpreted as being linked to a study about Y disease around the same time                                                                   | Plausible       | Minor          |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 14      | PA03.09, PA03.11, PA08.01.01, PA10.01, PA11.01       | L.2.2.1            | Sending samples to the technician known to be researching a specific disease could link the samples to that disease                                                                                                         | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 15      | PA03.09, PA03.11, PA08.01.01, PA10.01, PA11.01       | L.2.2.1            | Sending samples to the wet lab known to be researching a specific disease at that time could link the samples to that disease                                                                                               | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 26      | PA05.01.01                                           | I.2.1.1            | Nature of genomic data makes complete disassociability impossible to guarantee                                                                                                                                              | Plausible       | Moderate       |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 55      | PA03.09, PA09.01.01, PA09.01.03, PA09.01.04, PA11.01 | DD.4.1.2           | Bioinformatics tools come from a variety of developers that can change over time; corruption within this supply chain, especially if left unmonitored, could result in research subject data being disclosed                | Plausible       | Minor          |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+
   | 65      | PA02.02, PA07.05                                     | U.1.1              | Data subject does not clearly understand what data actions that analysis tools along the pipeline will perform on their data                                                                                                | Plausible       | Minor          |
   +---------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+----------------+

Once all validated threats have had feasibility and difficulty values assigned, the different combinations can be assigned normalized numerical values for ranking purposes, as shown in Table 18. Plausible attacks of negligible difficulty carry the highest value (resulting in higher priority) while implausible attacks of severe difficulty carry the lowest value (resulting in lower priority). To incorporate additional nuance into the rankings, weights were assigned to the LINDDUN threat types to reflect their relative severity in the context of genomic sequencing, as shown in Table 19. Note, though, that these values are purely an ordering mechanism and do not have any intrinsic meaning.

.. table:: Table 18. Attack Feasibility and Difficulty Combination Values

   +-----------------+----------------+-----------+--------------+-----------------+------------+
   | **Difficulty**  | **Negligible** | **Minor** | **Moderate** | **Significant** | **Severe** |
   |                 |                |           |              |                 |            |
   | **Feasibility** |                |           |              |                 |            |
   +=================+================+===========+==============+=================+============+
   | Plausible       | 1.0            | 0.8       | 0.6          | 0.4             | 0.2        |
   +-----------------+----------------+-----------+--------------+-----------------+------------+
   | Indeterminate   | 0.9            | 0.7       | 0.5          | 0.3             | 0.1        |
   +-----------------+----------------+-----------+--------------+-----------------+------------+
   | Implausible     | 0.8            | 0.6       | 0.4          | 0.2             | 0.0        |
   +-----------------+----------------+-----------+--------------+-----------------+------------+

.. table:: Table 19. LINDDUN Threat Weights

   +----------------------------------------------+-----------------------+
   | **LINDDUN Threat Type**                      | **Weight**            |
   +==============================================+=======================+
   | Data Disclosure                              | 1.0                   |
   +----------------------------------------------+-----------------------+
   | Identifying                                  | 0.85                  |
   +----------------------------------------------+-----------------------+
   | Linking                                      | 0.7                   |
   +----------------------------------------------+-----------------------+
   | Non-compliance                               | 0.5                   |
   +----------------------------------------------+-----------------------+
   | Unawareness and Unintervenability            | 0.5                   |
   +----------------------------------------------+-----------------------+
   | Detecting                                    | 0.3                   |
   +----------------------------------------------+-----------------------+
   | Non-repudiation                              | 0.2                   |
   +----------------------------------------------+-----------------------+

These values and weights were multiplied for each attack and the results used to rank order the threats in the core example from highest to lowest priority, as shown in Table 20. (Ties are resolved using attack number.) The prioritization of threats for the complete example is provided in `Appendix G <../Appendix/appendixG.html>`_. 

.. table:: Table 20. Core Example Threats in Ranked Order from Highest to Lowest Priority

   +---------+--------------------+-----------------+----------------+-------------------+
   | **No.** | **LINDDUN Threat** | **Feasibility** | **Difficulty** | **Ranking Value** |
   +=========+====================+=================+================+===================+
   | 55      | DD.4.1.2           | Plausible       | Minor          | 0.80              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 5       | L.2.1.2            | Plausible       | Minor          | 0.56              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 26      | I.2.1.1            | Plausible       | Moderate       | 0.51              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 1       | L.2.1.2            | Plausible       | Moderate       | 0.42              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 3       | L.2.1.2            | Plausible       | Moderate       | 0.42              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 4       | L2.1.2             | Plausible       | Moderate       | 0.42              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 14      | L.2.2.1            | Plausible       | Moderate       | 0.42              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 15      | L.2.2.1            | Plausible       | Moderate       | 0.42              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 65      | U.1.1              | Plausible       | Minor          | 0.40              |
   +---------+--------------------+-----------------+----------------+-------------------+
   | 2       | L.2.1.2            | Plausible       | Significant    | 0.28              |
   +---------+--------------------+-----------------+----------------+-------------------+

Given the limited number of threats in the *core* example, it would be reasonable to explicitly consider a response to each threat, including the option of acceptance. However, given that the number of threats in the complete example is an order of magnitude larger, some organizations may opt to accept threats below a certain priority threshold without further deliberation. Determining that threshold is a function of organizational tolerances and resources.

Response Determination
----------------------

High-priority threats tend to readily give rise to decisions to intervene (typically in the form of elimination or disruption). Likewise, low-priority threats tend to prompt decisions to accept the threat. In contrast, determining the appropriate response to threats occupying the middle ground—such as attack number 14—is often less straightforward.

Attack number 14 involves a seemingly unavoidable dataflow, so simply eliminating the dataflow is not an option, nor is there any obvious way of transferring responsibility. This leaves the option of either accepting the presence of the threat or disrupting it. Determining which course to pursue may require first exploring disruption options so that their viability may be considered.

There are several reference sources for such controls, but one of the most prominent is NIST Special Publication (SP) 800-53r5, Security and Privacy Controls for Information Systems and Organizations [Ref6]_. However, different organizations may have varying resources and expertise for selecting controls and control enhancements relevant to given threats. Though organizations may have different approaches to this process, the following describes a way of facilitating the process to map from individual PANOPTIC threat actions to candidate controls using the NIST Privacy Framework, leveraging NIST’s crosswalk [16]_ from PF Subcategories to 800-53 controls.

Handling a large number of candidate controls, even after duplicates are accounted for, requires a reduction step. One way of further constraining the effort is to focus on critical PANOPTIC threat actions. These are threat actions that others are dependent upon; disrupting critical threat actions in effect invalidates the attack. In attack number 14, the critical threat action is single source profiling. The threat actions that enable it (Recording and Biological sample) are unavoidable while the remaining threat actions (Affording revelations and Implication) are enabled by it. Focusing on single source profiling (and its associated LINDDUN threat) results in a set of less than 20 candidate controls. Appendix C shows this winnowing process, starting from the two PF Categories implicated by this threat action, mapping from the Categories to the relevant Subcategories, and from the Subcategories to the relevant 800-53 controls. 

Each Subcategory is augmented with an ordered tuple (e.g., [1 2 1 1]), representing the priority of that Subcategory for each of the four selected MOs drawn from the Genomic Data Profile [Ref5]_ (Organizational Tailoring in Appendix C provides more details of this approach). These tuples can be used to prioritize potential controls that might be employed to disrupt threats given that the Genomic Data Profile provides a list of MOs for organizations processing genomic data and prioritizes PF Subcategories (or outcomes) to support achieving those MOs. Based on the genomic sequencing workflow, four relevant MOs were selected: 

MO 2: Manage privacy risk to existing and future relatives

MO 3: Identify, model, and address cybersecurity and privacy risks of processing genomic data

MO 5: Manage privacy risk to donors

MO 12: Promote the use of privacy-enhancing technologies as well as secure technologies for sharing genomic data

Each Privacy Framework Subcategory includes this tuple that indicates the Genomic Data Profile prioritization of MO 2, MO 3, MO 5, and MO 12 listed as [1 2 1 2].

.. table:: Table 21. Mapping from Single Source Profiling to SP 800-53r5 Controls

   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | **Privacy Framework Function - Category** | **Privacy Framework Subcategory**                                                                                                      | **800-53 Controls** | **800-53 Control Family**             |
   +===========================================+========================================================================================================================================+=====================+=======================================+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | AC-23               | Access Control                        |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | AU-3(3)             | Audit and Accountability              |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | IA-4(8)             | Identification and Authentication     |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | PE-8(3)             | Physical and Environmental Protection |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | SA-8(33)            | System and Services Acquisition       |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P2: Data are processed to limit the identification of individuals [1 2 1 2]                                                      | SI-12(1)            | System and Information Integrity      |
   |                                           |                                                                                                                                        |                     |                                       |
   |                                           |                                                                                                                                        | SI-12(2)            |                                       |
   |                                           |                                                                                                                                        |                     |                                       |
   |                                           |                                                                                                                                        | SI-19               |                                       |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | AC-23               | Access Control                        |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | AU-16(3)            | Audit and Accountability              |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | IA-8(6)             | Identification and Authentication     |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | PL-8                | Planning                              |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | PM-7                | Program Management                    |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | SA-8(33)            | System and Services Acquisition       |
   |                                           |                                                                                                                                        |                     |                                       |
   |                                           |                                                                                                                                        | SA-17               |                                       |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | SC-2(2)             | System and Communications Protection  |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Control-P – Disassociated Processing      | CT.DP-P3: Data are processed to limit the formulation of inferences about individuals’ behavior or activities [2 3 2 2]                | SI-19               | System and Information Integrity      |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Protect-P – Protective Technology         | PR.PT-P2: The principle of least functionality is incorporated by configuring systems to provide only essential capabilities [3 2 2 2] | AC-3                | Access Control                        |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+
   | Protect-P – Protective Technology         | PR.PT-P2: The principle of least functionality is incorporated by configuring systems to provide only essential capabilities [3 2 2 2] | CM-7                | Configuration Management              |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------------------------+

Once the set of potentially applicable controls has been narrowed down in this way, the tuples derived from MO 2, MO 3, MO 5, and MO 12 can be used to prioritize the Subcategories and by extension control selection. [17]_  MO 2, which deals with privacy risk to relatives, is not relevant for this attack and can be ignored. MO 12, which addresses use of privacy-enhancing technologies (PETs), assigns the same priority to all three Subcategories and can also be ignored as it does not contribute any differentiation. The prioritizations for MO 3 and MO 5, however, readily yield an ordering of (1) CT.D-P2 [2 1], (2) PR.PT-P2 [2 2], (3) CT.DP-P3 [3 2].

Reviewing the controls associated with CT.DP-P2 for those that appear most relevant or impactful, we find two candidates:

- IA-4(8) Pairwise Pseudonymous Identifiers − Generate pairwise pseudonymous identifiers.

- SI-12(1) Limit Personally Identifiable Information Elements − Limit personally identifiable information being processed in the information life cycle to the following elements of PII: [Assignment: organization-defined elements of personally identifiable information].

Reviewing the controls associated with PR.PT-P2, we find:

- CM-7 Least Functionality − Configure the system to provide only [Assignment: organization-defined mission essential capabilities].

Finally, reviewing the controls associated with CT.DP-P3, we find:

- AU-16(3) Disassociability − Implement [Assignment: organization-defined measures] to disassociate individuals from audit information transmitted across organizational boundaries.

All of these in various ways could help prevent the association of identifiable individuals with specific studies or tests. However, the most direct ones are arguably those associated with the highest priority Subcategory, CT.DP-P2. Both of these point toward the need to break the link between specific individuals and (inferred) specific lab operations. Employing pairwise pseudonymous identifiers as per IA-4(8) (generating a unique identifier for every sample, even if the samples pertain to the same data subject) could accomplish this if samples could be pseudonymized at the source. This would involve the client interacting with a sequencing service system (possibly via an application programming interface, API) to generate the pseudonymous identifier that would be used for shipping purposes. The receiving clerk would then enter/scan the identifier into the system, but with restricted access to information (SI-12(1)) and functionality (CM-7), to determine which lab technician should receive it. This approach could possibly leverage an existing interface (e.g., a Web portal used for communicating results).

While in this case one might well have arrived at the same or similar conclusions without the Subcategory prioritization, some of the threat actions map to a significantly greater number of Subcategories with a much larger set of associated controls. In those cases, Subcategory prioritization can provide beneficial structure that facilitates control selection. Where there are many Subcategories, prioritization might even provide a basis for limiting control selection to those associated with the higher-priority Subcategories.  

It stands to reason that similar threats should respond to similar interventions, so in principle these disruptions should be applicable to all instances of the scenario, addressing attacks 1 through 5 as well as attack number 15. This also applies to other intervention types. One might also potentially identify similar attacks in different scenarios by searching on the associated critical threat actions and/or specific LINDDUN threats. Further, selection of controls that show up frequently across disruptions may offer greater cost-effectiveness, as long as care is taken to ensure that all targeted threats are sufficiently addressed. Also, given that some threats involve 3rd parties, controls that focus on agreements or those such as CA-02 Control Assessments and CA-03 Information Exchange may offer interventions that address multiple threats. 

.. [16]
   https://github.com/usnistgov/PrivacyFrmwkResources/raw/master/resources/NIST%20SP%20800-53%20Crosswalk/csf-pf-to-sp800-53r5-mappings.xlsx 

.. [17]
   While in principle the Mission Objectives could be employed to prioritize threats rather than controls, the MOs selected for this workflow provide insufficient differentiation; MOs 3, 5, and 12 will be implicated by most threats.