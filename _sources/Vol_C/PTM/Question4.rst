Question 4: "Did we do a good job?"
===================================

Question 4, “Did we do a good job?” directs the project team to evaluate the effectiveness of answers to Questions 1-3. This paper outlines the effort to document genomic data processing environments from a privacy standpoint (Question 1), identify genomic data threats to privacy (Question 2), and implement interventions (Question 3). The threat modeling process is designed to be iterative. This paper showcases the process rather than an exhaustive analysis to guide other teams conducting genomic data threat modeling for privacy on their own systems. Question 4 also helps emphasize that this process will be repeated to address changes in the system and threat environments. 

This section provides guidelines on how to address Question 4 and suggests additional activities that can be used by teams to evaluate their efforts. The threat modeling documentation in the form of adapted PRAM Worksheets 1 and 2 should be reviewed and updated periodically to address new threats, system changes, new assumptions, and changes in risk tolerance.

Did We Do a Good Job Documenting the System and Its Data Actions?
-----------------------------------------------------------------

`Question 1 <Question1.html>`__ documents the system context, including PANOPTIC Contextual Domain mappings and DFDs. DFDs directly support threat identification and analysis while Contextual Domain mappings indirectly support the process. In comparison to cybersecurity threat modeling, threats related to privacy can arise from systems operating as designed therefore trust boundaries are a concept that is not used. As such, the entirety of the system is potentially relevant for privacy analysis.

The following activities could potentially improve the documentation of the system and its data actions:

- Review the system scope to ensure that it has captured the full breadth of data and data actions.

- Check whether contextual information is sufficiently specific.

- Check whether DFDs are sufficiently detailed to capture communications between systems and all data actions. 

- Review documentation and information from suppliers, developers, and users—including that addressing data subject consents and preferences—to consider any updates required.

- Review change control processes to ensure that changes are documented properly.

- Update the documentation to reflect changes to the system context or dataflows, including system interconnections, devices added, or issues identified through testing or monitoring.

- Review data handling processes to ensure adherence to best practices and reflect any changes in the contextual information or DFDs as applicable.

Did we do a good job identifying and documenting threats?
---------------------------------------------------------

To answer, “Did we do a good job?” on Question 2, “What could go wrong?” the project team evaluated whether the threat model adequately identified and documented threats to data subjects. `Question 2 <Question2.html>`__ enumerates the threats identified for the core example based on the LINDDUN dataflow analysis and the PANOPTIC attacks, with the results for the complete example documented in `Appendix F <../Appendix/appendixF.html>`_. The following actions could improve threat identification.

**Evaluate the comprehensiveness of the LINDDUN analysis.** The LINDDUN per element threat mapping heuristic shown in Table 11 acts as a completeness check. With this table, a completeness check can be done for the typical threats against external entities, processes, data stores, and dataflows. If there are possible threats that were not considered by the team, this highlights an area for additional consideration. Maintaining a checklist for each dataflow segment by making and marking copies of Table 11 could help prevent potentially relevant threats from being overlooked.

**Evaluate the comprehensiveness of the identified PANOPTIC threat actions.** When evaluating the PANOPTIC attacks:

- Consider attacks that have occurred in the genomic stakeholder community and closely adjacent industries. Threat intelligence can be used to identify attacks favored by actors who are known to target an industry. The Bioeconomy Information Sharing and Analysis Center (BIO-ISAC) is one potential source of such intelligence. [18]_ 

- Consider whether the identified scenarios and selected PANOPTIC threat actions reflect these attacks, or if additional scenarios and/or threat actions should be considered.  

- Determine whether the threats being considered adequately reflect the threats listed in published documents for the genomic community, such as NIST IR 8432 [Ref11]_.

**Review and confirm that invalidated threats are in fact invalid.** Revisit invalidated threats to ensure that they were not mistakenly invalidated because a relevant LINDDUN threat was overlooked, or a relevant PEO was not recognized as such. To facilitate such a review, it is essential to retain documentation of invalidated threats.

**Review organizational policies, strategies, and processes to determine if there are other threat areas not being addressed by the technical evaluation.** Such a review may uncover otherwise overlooked but relevant activities or scenarios. For example, sharing of data for ancillary purposes could take place via mechanisms largely separate from the target system, such as copying of LIMS logs. If the sequencing service is actively seeking to be acquired, that could potentially present threats related to any retained samples or data.

Did we do a good job mitigating the threats?
--------------------------------------------

`Question 3 <Question3.html>`__ discussed the kinds of responses to the identified threats that might be considered. More specifically, using one of the attacks in the core example, it illustrated how to intervene by disrupting the threat using standard controls by reasoning from the attack to particular controls by way of the NIST PF.

The following actions could evaluate and improve on this approach:

- Review interventions to assess how well they address the LINDDUN threats associated with the attacks.

- Expand interventions to cover additional PF Subcategories beyond those that were addressed based on the prioritizations in the Genomic Data Profile for the Mission Objectives that have been established. (See `Organizational Tailoring in Appendix C <../Appendix/appendixC.html#organizational-tailoring>`__.)

- Review the documentation from Question 1 to check which, if any, interventions may already be present.

- If the answers to Questions 1 and/or 2 have changed, revisit the relevant response determinations.

- Develop a surveillance plan that incorporates any findings from assessments, tabletop exercises, or ongoing vulnerability monitoring using available resources [19]_ and documents how they will be integrated into future threat modeling activities.

Additional Activities
---------------------

The following additional actions help evaluate the thoroughness of responses and regularly consider the impact of any changes to the system or threat environment. A legal review may be appropriate to determine if the interventions, accepted threats, and transferred responsibilities (particularly the manner of transfer notification) meet the necessary regulatory requirements (GV.PO-P).

**Review Threat Responses.** Appropriate documentation of threat responses beyond disruption is critical to ensuring that they can be revisited as circumstances change.

- **Eliminate.** Eliminating threats often removes features. Accompanying documentation should justify the trade-offs involved. This documentation is necessary because threat models will need to be revisited as the system and organization evolves. Future threat modeling efforts may involve different participants who may not be familiar with the system and will rely on this documentation.

- **Accept.** Threats that are accepted should be documented sufficiently to explain why. For example, the interventions necessary to disrupt attack number 1 and similar attacks in the core example, where sending a group of samples together to the same technician could link the samples to the disease they’re known to be researching, may be considered too onerous relative to the threat’s priority. The reason for the threat acceptance needs to be documented so that if the process surrounding sample intake changes, the threat and the response to it can be reassessed.

- **Transfer.** When responsibility for threats is transferred, documentation should clearly indicate the entity assuming accountability for those threats. That entity may then choose to intervene, accept, or further transfer responsibility for the threat. Documentation adequately specifies the obligations and expectations of both parties. Note that not all responsibilities can be transferred, such as those which are legally obligated (e.g., breach notification).

**Update DFDs.** As interventions are added, DFDs may need to be updated. The possibility of new threats against changed or added elements should be considered. If new threats arise from changes, appropriate responses must be determined, which could include reconsidering the intervention.

**Review PANOPTIC Attacks.** If there are interventions in place that disrupt multiple common threat actions, that can be a positive indication of the layering of controls, which supports robust privacy protection.

**Utilize Framework Profiles.** Teams can use the Genomic Data Profile to identify further interventions by considering additional priority Subcategories for each relevant Mission Objective. (See `Organizational Tailoring in Appendix C <../Appendix/appendixC.html#organizational-tailoring>`__.) Alternatively, PF Subcategories associated with the disruptions selected during Question 3 activities can be used to inform an organization’s PF Target Profile, which could leverage a Community Profile such as the Genomic Data Profile. The organization can then identify potential gaps by comparing its Current Profile to its Target Profile.

**Track Interventions Throughout the System Life Cycle.** Threat interventions should be documented, reviewed, tested, and maintained as the threat environment changes. This may include the following considerations:

- During the implementation phase, threat modeling should be periodically revisited and updated. Consider whether the intervention caused problems and if so, what were the impacts.  

- Once interventions are operational, consider their effectiveness and any unanticipated negative impact to Mission Objectives. For example, if the intervention reduced the ability of direct data subjects to exercise control over their data (CT.PO-P3), consider if the protection provided by the intervention justified that diminution of control.

- Organizations should update their threat response and possibly the relevant aspects of their threat model after an intervention fails, considering whether the failure resulted from erroneous analysis. Performing and documenting root cause analysis can usefully inform future decisions.

- Privacy assessment, including automated and manual red teaming, is another useful tool to evaluate how the interventions and threat modeling perform and how they can be improved. 

- •	Tabletop and functional exercises as described in SP 800-84 [Ref12]_ can also be very helpful in evaluating Question 3 performance and can be done both before and after a system is in use.

.. [18]
    https://www.isac.bio/

.. [19]
    https://nvd.nist.gov