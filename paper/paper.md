---
title: 'BioHackEU25 report: Towards a Robust Validation Service for Data and Metadata in ARC RO-Crates'
title_short: 'BioHackEU25 #28: ARC Metadata Validation'
tags:
  - FDO
  - ARC
  - RO-Crate
  - SHACL
  - Frictionless
  - FAIRDOM-Seek
  - ISA
authors:
  - name: Eli Chadwick
    orcid: 0000-0002-0035-6475
    affiliation: 1
    role: Project Administration, Supervision, Data Curation, Investigation, Writing - review & editing
  - name: Matthijs Brouwer
    orcid: 0000-0001-8183-0484
    affiliation: 2
    role: Project Administration, Supervision, Data Curation, Investigation, Writing - review & editing
  - name: Kevin Schneider
    orcid: 0000-0002-2198-5262
    affiliation: 3
    role: Project Administration, Supervision, Data Curation, Investigation, Writing - review & editing
  - name: Daniel Arend
    orcid: 0000-0002-2455-5938
    affiliation: 4
    role: Conceptualization
  - name: Finn Bacall
    orcid: 0000-0002-0048-3300
    affiliation: 1
    role: Data Curation, Investigation
  - name: Etienne Bardet
    orcid: 0009-0006-6288-4173
    affiliation: 5
    role: Data Curation
  - name: Sebastian Beier
    orcid: 0000-0002-2177-8781
    affiliation: 6
    role: Conceptualization, Writing - original draft 
  - name: Dominik Brilhaus
    orcid: 0000-0001-9021-3197
    affiliation: 7
    role: Data Curation, Investigation
  - name: Xiaoming Hu
    orcid: 0000-0002-8318-3222
    affiliation: 8
    role: Data Curation
  - name: Emma Le Roy Pardonche
    orcid:
    affiliation: 5
    role: Data Curation
  - name: Timo Mühlhaus
    orcid: 0000-0003-3925-6778
    affiliation: 3
    role: Supervision, Investigation
  - name: Stuart Owen
    orcid: 0000-0003-2130-0865
    affiliation: 1
    role: Data Curation, Investigation
  - name: Cyril Pommier
    orcid: 0000-0002-9040-8733
    affiliation: 5
    role: Supervision, Investigation, Writing - review & editing
  - name: Heinrich Lukas Weil
    orcid: 0000-0003-1945-6342
    affiliation: 3
    role: Data Curation, Investigation

affiliations:
  - name: Department of Computer Science, The University of Manchester, United Kingdom
    index: 1
  - name: Department of Plant Breeding, Wageningen University & Research, Netherlands
    index: 2
  - name: Computational Systems Biology, Rheinland-Pfälzische Technische Universität Kaiserslautern-Landau, Germany
    index: 3
  - name: Leibniz Institute for Plant Genetics and Crop Plant Research (IPK) Gatersleben, Germany
    index: 4
  - name: Université Paris-Saclay, INRAE, URGI, France
    index: 5
  - name: Institute of Bio- and Geosciences (IBG-4 Bioinformatics), Bioeconomy Science Center (BioSC), CEPLAS, Forschungszentrum Jülich GmbH, 52425 Jülich, Germany
    index: 6
  - name: Cluster of Excellence on Plant Sciences (CEPLAS) / Heinrich-Heine-University Düsseldorf, Germany
    index: 7
  - name: Scientific Databases and Visualization, Heidelberg Institute for Theoretical Studies, 69118 Heidelberg, Germany
    index: 8
    
date: 07 November 2025
cito-bibliography: paper.bib
event: BH25EU
biohackathon_name: "BioHackathon Europe 2025"
biohackathon_url:   "https://biohackathon-europe.org/"
biohackathon_location: "Berlin, Germany, 2025"
group: Project 28
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/sebeier/bhe25_project28
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Chadwick \emph{et al.}
---


# Introduction

As part of the BioHackathon Europe 2025, we here report about the progress of project 28 during the event.

## Abstract - Towards a Robust Validation Service for Data and Metadata in ARC RO-Crates

Robust validation of both research data and its accompanying metadata is essential for ensuring adherence to FAIR principles. Current approaches often handle these aspects separately, hindering a holistic quality assessment. Building upon (previous BioHackathon work)[@citesAsAuthority:beier2025biohackgermany24] [@citesAsAuthority:arend2022biohackeu22] [@citesAsAuthority:arend2023] establishing (Annotated Research Contexts)[@citesAsAuthority:dataplant_2025_15197625] as (RO-Crates)[@citesAsAuthority:10.3233/ds-210053] - (ARC RO-Crate)[@citesAsAuthority:beier2025biohackeu24] - , we aim to develop and demonstrate an integrated validation strategy for FAIR digital objects. It distinguishes between validating the metadata descriptor and the payload data files.

For the metadata descriptor, validation will ensure structural and semantic compliance to the base RO-Crate specification and the ARC-ISA family of RO-Crate profiles, using and extending the RO-Crate validator tool.

For the payload data files, validation targets the actual content, since data files often require domain-specific structural and value constraints, which requires explicit schema definitions. For this, we will integrate Frictionless for checking data content against community standards (e.g. (MIAPPE)[@citesAsAuthority:Papoutsoglou2020], as demonstrated in the HORIZON project AGENT). Crucially, this project will also explore mechanisms for specifying expected data structures’ requirements within the ARC RO-Crate itself. This aims to provide a more self-contained description of data, investigating how such internal requirements can be linked to data validation frameworks, complementing the crate’s metadata validation.

The overall goal is to provide a powerful, holistic validation mechanism for ARC RO-Crates, enhancing their reliability, trustworthiness, and FAIRness. A MIAPPE-compliant plant phenomics dataset will serve as a use case. This integrated validation approach aims to streamline quality control for researchers and will be packaged as a deployable microservice, offering broad applicability across diverse research workflows.

# Results

During the BioHackathon, we split our work into four parallel tracks: (1) Metadata-level validation using SHACL, (2) Payload data-level validation using Frictionless Data specifications, and (3) The development of RO-Crate Profiles to define the standards being validated against. (4) Implementation of ISA-structured RO-Crate export in (FAIRDOM-SEEK)[@citesAsAuthority:wolstencroft2015seek].

## (1) Metadata Validation (SHACL)

The validation of the RO-Crate metadata structure (i.e., the `ro-crate-metadata.json` file) against specific profiles is crucial for semantic interoperability. We confirmed the strategy of using SHACL (Shapes Constraint Language) for this purpose.

Work focused on the existing `rocrate-validator` tool with the goal of extending it to support more profiles, specifically the (ISA)[@citesAsAuthority:Rocca_Serra2010] and new MIAPPE profiles being developed (see track 3). This involved planning and initial work on teaching the validator to recognize and apply these new profile definitions, ensuring that crates claiming to conform to a profile (e.g., the ISA structure) actually do.

[Eli to add something about our attempts to use ro-crate-schema-tools]

## (2) Payload Data Validation (Frictionless)

For validating the contents of payload files (e.g., tabular data in XLSX or CSV files), we adopted the Frictionless Data framework.

* **Datamap validation**: We established the [`datamap-validation` tool](https://https://github.com/kMutagene/biohack_eu_2025_p28/tree/main/datamap-validation) to convert an [ARC Datamap](https://nfdi4plants.github.io/nfdi4plants.knowledgebase/arctrl/datamap/#_top) - a metadata descriptor format for payload in ARCs that uses data fragment descriptors to add ontology annotations to any part of a file - into a Frictionless tableschema - the schema format that is used by Frictionless to validate tabular data. Subsequently, every file annotated by the Datamap is then validated against this schema, and a junit xml report is generated. The tool is containerized and (currently) hosted on [dockerhub](https://hub.docker.com/r/mutagene/datamap-validation/tags.).

![Picture1](https://hackmd.io/_uploads/S1nLT6sJbx.png)

* **DataHUB integration**: 

As the `datamap-validation` tool is containerized, it can be used in CI/CD pipelines on the DataHUB (a collaborative cloud platform to host and share ARCs) [@citesAsAuthority:Weil2023]. The generated junit xml report can be displayed on each job. The following snippet contains a suggestion on how to integrate this in an ARC via the `.gitlab-ci.yml` file without turning off other integrations:

```yml
include:
    - template: Auto-DevOps.gitlab-ci.yml

stages:
    # stages from default integrations
    - arc_json
    - quality_report_generator
    - quality_report
    - generate_metadata
    # custom datamap validation
    - datamap-validation

Datamap Validation:
    stage: datamap-validation
    image: mutagene/datamap-validation:latest
    script:
        - python /app/datamap-validation.py --arc-path ./ --out-path \
          ./junit_report.xml
    artifacts:
        when: always
        paths:
            - junit_report.xml
        reports:
            junit: junit_report.xml

```



* **Tooling**: We used and bugfixed the `excel-validator` tool, which leverages Frictionless, and applied it to real-world MIAPPE-compliant XLSX datasets. This allowed us to write datamaps for existing datasets and generate the corresponding Frictionless schemas.



## (3) RO-Crate Profile Development

A significant effort was dedicated to defining and creating machine-actionable RO-Crate Profiles for the domains of interest.

* **ISA RO-Crate Profile**: We successfully created a "Profile Crate" for the ISA (Investigation-Study-Assay) structure. This is an RO-Crate that defines the ISA RO-Crate Profile itself, making it discoverable and reusable. A helper script was also developed to aid in the creation of such Profile Crates.

* **RO-Crate Profile Crate Creator**: To aid in this process, we developed the `RO-Crate Profile Crate Creator` (https://github.com/nfdi4plants/ROCratePCC), a new polyglot library (available for Python, .NET, and JavaScript) that programmatically generates the ro-crate-metadata.json for a profile based on a set of inputs.

* **MIAPPE RO-Crate Profile**: A dedicated subgroup worked on defining a new [RO-Crate profile for MIAPPE](https://github.com/MIAPPE/MIAPPE-ROCrate/blob/main/MIAPPE_ro_crate.md) (Minimum Information About a Plant Phenotyping Experiment). This involved:

    * Refactoring biological material definitions to align ISA and MIAPPE (e.g., mapping `ISA Source` to `Material Source` and `ISA Sample` to `Biological Material`).

    * Defining the use of `PropertyValue` for MIAPPE parameters.

    * Concluding that a new "MIAPPE ARC RO-Crate Profile" is required, which will inherit from the ISA, ARC and Datamap profiles (as a direct decendent of the ARC profile).

* **Workflow RO-Crate Profile**: The existing Workflow RO-Crate profile was updated to support RO-Crate version 1.2 (https://doi.org/10.5281/zenodo.13751027), which was released in June 2025. This will enable the Workflow Run Crate profiles and other profiles which build on Workflow RO-Crate to also support RO-Crate 1.2. 

## (4) ISA RO-Crate Export in FAIRDOM-SEEK

Implemented RO-Crate export functionalities in SEEK with ISA profile compliance, establishing the fountation for Investigation-Study-Assay data packaging and validation. 

* Built comprehensive test suite using [ro-crate-ruby](https://github.com/ResearchObject/ro-crate-ruby) gem. 
* JERM ontology types are correctly mapped for ISA entities. 
* Extended Metadata is converted into `schema:PropertyValue` format and embedded in the RO-Crate for each ISA entity.


## Tooling and Implementations

Parallel work included experimenting with `ro-crate-ruby` to generate assay-level RO-Crates and include extended metadata directly within the crate.

## Validation Strategy Considerations

A key activity was evaluating the different strategies for profile validation. Our goal was to find a method that is not only powerful but also accessible to profile developers who may not be RDF experts.

* **Hand-compiled SHACL**: The current approach of the `rocrate-validator`, which our project aimed to extend. It is powerful but has a steep learning curve and can be complex to author and debug.

* **SoSS-based Profiles**: We reviewed a prototype (`ro-crate-schema-tools`) from the Australian [LDaCA](https://ardc.edu.au/project/language-data-commons-of-australia) team, which proposes extending the existing Schema.org Style Schema (SoSS) approach. This aims for a declarative, JSON-LD native method that could be easier to implement and drive tooling (like editors) directly from the profile.

* **LinkML**: Prior investigation by our group explored LinkML as a user-friendly (YAML-based) alternative to generate SHACL. While promising, this was found to be unviable for now due to significant limitations in the LinkML-to-SHACL generator. Key challenges included poor support for RO-Crate patterns like multi-typing (having multiple values for `@type`) and other required features not being supported by the conversion tooling.

* **Other proposals**: We also noted other proposals in the community, such as Michael Milton's crate-compatible SHACL profile and Simon Taurus's JSON-Schema based approach.

This review informed our own profile development (Track 3) and confirmed the need for specialized `PropertyValue` definitions (e.g., for DOIs and PubmedIDs) to improve semantic precision, a feature discussed for the `isa-ro-crate-profile`.

# Discussion

The BioHackathon was highly productive. We successfully defined the architecture for a two-pronged validation system (metadata and data) and made significant progress on the required components.

The data validation track (Frictionless schema conversion) is largely complete. The MIAPPE and ISA profile definitions are well-advanced. The primary remaining tasks are to finalize the `rocrate-validator` extension to use these new profiles and to develop the "Profile Crate creator" tool further.

## Next Steps

Our immediate next steps are:

1. Finalize and publish the ISA and MIAPPE ARC RO-Crate profiles.

2. Complete the extension of the `rocrate-validator` to dynamically load and apply these profiles.

3. Package the Frictionless validation path (DataMap to tableschema) into a deployable microservice.

4. Integrate these validation services into DataHUB CI/CD pipelines, triggered by the new entry points in the Workflow Run Crate profile.

5. Integrate new ISA exporter into FAIRDOM-SEEK’s core, and add ISA profile validation.

This project provides a clear path towards a holistic validation mechanism for ARC RO-Crates, significantly enhancing their FAIRness and reliability.

## Acknowledgements

We thank the organizers of the BioHackathon Europe 2025. This work was funded by ELIXIR, the research infrastructure for life-science data; by the Federal Government of Germany and the county of North Rhine-Westphalia (de.NBI - the German Network for Bioinformatics Infrastructure); by the German Research Foundation (DFG) within the project “Establishment of the National Research Data Infrastructure (NFDI)” in the consortium DataPLANT (https://www.nfdi4plants.de/, project number 442077441) and FAIRagro (www.fairagro.net, project number 501899475); and the European Union through Horizon Europe grant agreement 101094287 (BIOINDUSTRY 4.0) and Horizon 2020 research and innovation programme under grant agreement No. 862613 (AGENT).

We acknowledge the extensive discussions with the members of the Language Data Commons of Australia on machine-actionable profiles and validation strategies.


## References
