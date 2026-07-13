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
    orcid: 0009-0006-3181-0059
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
    ror: 027m9bs27
  - name: Department of Plant Breeding, Wageningen University & Research, Netherlands
    index: 2
    ror: 04qw24q55
  - name: Computational Systems Biology, Rheinland-Pfälzische Technische Universität Kaiserslautern-Landau, Germany
    index: 3
    ror: 01qrts582 
  - name: Leibniz Institute for Plant Genetics and Crop Plant Research (IPK) Gatersleben, Germany
    index: 4
    ror: 02skbsp27
  - name: Université Paris-Saclay, INRAE, URGI, France
    index: 5
    ror: 003vg9w96
  - name: Institute of Bio- and Geosciences (IBG-4 Bioinformatics), Bioeconomy Science Center (BioSC), CEPLAS, Forschungszentrum Jülich GmbH, 52425 Jülich, Germany
    index: 6
    ror: 02nv7yv05
  - name: Cluster of Excellence on Plant Sciences (CEPLAS) / Heinrich-Heine-University Düsseldorf, Germany
    index: 7
    ror: 034waa237
  - name: Scientific Databases and Visualization, Heidelberg Institute for Theoretical Studies, 69118 Heidelberg, Germany
    index: 8
    ror: 01f7bcy98
    
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

As part of the BioHackathon Europe 2025, we here report about the progress of project 28 during the event. The concept and technical foundations for this work were initially funded and developed through the HARVEST project (within the BFSP scientific programme), and the effort was concluded during the BioHackathon.

## Towards a Robust Validation Service for Data and Metadata in ARC RO-Crates

Robust validation of both research data and its accompanying metadata is essential for ensuring adherence to FAIR principles. Current approaches often handle these aspects separately, hindering a holistic quality assessment. Building upon (previous BioHackathon work)[@citesAsAuthority:beier2025biohackgermany24] [@citesAsAuthority:arend2022biohackeu22] [@citesAsAuthority:arend2023] establishing (Annotated Research Contexts)[@citesAsAuthority:dataplant_2025_15197625] as (RO-Crates)[@citesAsAuthority:10.3233/ds-210053] - (ARC RO-Crate)[@citesAsAuthority:beier2025biohackeu24] - , we aim to develop and demonstrate an integrated validation strategy for these FAIR Digital Objects. It distinguishes between validating the metadata of the dataset and validating the payload data files.

For the metadata, validation will ensure structural and semantic compliance to the base RO-Crate specification and the ARC family of RO-Crate profiles, including the ISA, Workflow-Run and Datamap profiles, using and extending the [`rocrate-validator`](https://github.com/crs4/rocrate-validator) tool [@citesAsRelated:rocrate-validator], which uses SHACL (Shapes Constraint Language) [@citesAsRelated:shacl] and Python to validate RO-Crate metadata.

For the payload data files, validation targets the actual content, since data files often require domain-specific structural and value constraints, which requires explicit schema definitions. For this, we will integrate [Frictionless](https://frictionlessdata.io) for checking data content against community standards (e.g. Minimum Information About a Plant Phenotyping Experiment (MIAPPE)[@citesAsAuthority:Papoutsoglou2020], as demonstrated in the HORIZON project AGENT). Crucially, this project will also explore mechanisms for specifying expected data structures’ requirements within the ARC RO-Crate itself. This aims to provide a more self-contained description of data, investigating how such internal requirements can be linked to data validation frameworks, complementing the RO-Crate’s metadata validation.

The overall goal is to provide a powerful, holistic validation mechanism for ARC RO-Crates, enhancing their reliability, trustworthiness, and FAIRness. A MIAPPE-compliant plant phenomics dataset will serve as a use case. This integrated validation approach aims to streamline quality control for researchers and will be packaged as a deployable microservice, offering broad applicability across diverse research workflows.

# Results

During the BioHackathon, we split our work into four parallel tracks: 

1. Metadata-level validation using SHACL
2. Payload data-level validation using Frictionless Data specifications
3. The development of RO-Crate Profiles to define the standards being validated against
4. Implementation of ISA-structured RO-Crate export in (FAIRDOM-SEEK)[@citesAsAuthority:wolstencroft2015seek].

## (1) Metadata Validation (SHACL)

The validation of the RO-Crate metadata structure (i.e. the contents of the `ro-crate-metadata.json` file) against specific profiles is crucial for semantic interoperability. We confirmed the strategy of using SHACL  for this purpose, and have continued in this direction since the hackathon.

Work focused on the existing `rocrate-validator` tool with the goal of extending it to support more profiles, specifically the (ISA)[@citesAsAuthority:Rocca_Serra2010] and new MIAPPE profiles being developed (see track 3). This involved planning and initial work on teaching the validator to recognize and apply these new profile definitions, ensuring that crates claiming to conform to a profile (e.g. the ISA structure) actually do.

Other metadata validation methods were investigated but found to be less practical at this time; these are described in more detail in [Validation Strategy Considerations](#Validation-Strategy-Considerations) below.

## (2) Payload Data Validation (Frictionless)

For validating the contents of payload files (e.g. tabular data in XLSX or CSV files), we adopted the Frictionless Data framework.

* **Datamap validation**: [ARC Datamap](https://nfdi4plants.github.io/nfdi4plants.knowledgebase/arctrl/datamap/#_top) is a metadata descriptor format for ARC payloads that uses data fragment descriptors to add ontology annotations to any part of a file. We established the [`datamap-validation` tool](https://github.com/kMutagene/biohack_eu_2025_p28/tree/main/datamap-validation) to convert an ARC Datamap into a Frictionless tableschema - the schema format that is used by Frictionless to validate tabular data. Subsequently, every file annotated by the Datamap is then validated against this schema, and a junit xml report is generated. The tool is containerized and (currently) hosted on [Dockerhub](https://hub.docker.com/r/mutagene/datamap-validation/tags).

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
    script: |
        - python /app/datamap-validation.py \
        --arc-path ./ \
        --out-path ./junit_report.xml
    artifacts:
        when: always
        paths:
            - junit_report.xml
        reports:
            junit: junit_report.xml

```



* **Tooling**: We used and bugfixed the `excel-validator` [@citesAsRelated:excel-validator] tool, which leverages Frictionless, and applied it to real-world MIAPPE-compliant XLSX datasets. This allowed us to write datamaps for existing datasets and generate the corresponding Frictionless schemas.



## (3) RO-Crate Profile Development

A significant effort was dedicated to defining and creating machine-actionable RO-Crate Profiles for the domains of interest.

* **ISA RO-Crate Profile**: We successfully created a "Profile Crate" for the ISA (Investigation-Study-Assay) structure. This is an RO-Crate that defines the ISA RO-Crate Profile itself, making it discoverable and reusable. A helper script was also developed to aid in the creation of further Profile Crates (see next item).

* **RO-Crate Profile Crate Creator**: To aid in the creation of a collection of Profile Crates for different RO-Crate profiles, we developed the `RO-Crate Profile Crate Creator` (https://github.com/nfdi4plants/ROCratePCC), a library that programmatically generates the `ro-crate-metadata.json` for a profile based on the guidelines in the RO-Crate specification [@citesAsAuthority:10.3233/ds-210053]. The user provides paths to the profile specification, examples, and other related material, and the library connects them together in the RO-Crate metadata, avoiding the complexity involved in doing this manually.`ROCratePCC` is written in F# and available for Python, .NET, and JavaScript.

* **MIAPPE RO-Crate Profile**: A dedicated subgroup worked on defining a new [RO-Crate profile for MIAPPE](https://github.com/MIAPPE/MIAPPE-ROCrate/tree/main)  based on the ISA RO-Crate profile (https://github.com/nfdi4plants/isa-ro-crate-profile). This was motivated by the fact, that not all information required for MIAPPE compliance can be represented by the existing ISA RO-Crate profile. As a consequence, two profiles are being developed and tested in parallel in dedicated github branches.
    * [MIAPPE aligned profile](https://github.com/MIAPPE/MIAPPE-ROCrate/tree/MIAPPE_ROcrate) which uses the mapping of MIAPPE with Schema.org and Bioschemas. It is a straightforward implementation that reuse the definitions and data model developed for plant scientists in the MIAPPE community. 
    * [ISA MIAPPE profile](https://github.com/MIAPPE/MIAPPE-ROCrate/tree/ISA_MIAPPE_ROcrate) which is a more generic extension of the ARC RO-Crate profiles. It models MIAPPE properties using ontology driven `PropertyValue` inspired by ISA. The biological material definitions have been refactored to align ISA and MIAPPE (e.g. mapping `ISA Source` to `Material Source` and `ISA Sample` to `Biological Material`). The [ARC Datamap RO-Crate profile](https://github.com/nfdi4plants/arc-datamap-ro-crate-profile) have been slightly adjusted to better suit MIAPPE `Observation Units`. The MIAPPE `Biological Material` definitions are stored in `LabProcess` objects. A new "MIAPPE ARC RO-Crate Profile" is required in some form or another, which will inherit from the ARC ISA and Datamap profiles (as a direct decendent of the ARC profile). If possible, this profile would not require definition of new properties, but would only contain guidance and constraints on how existing properties are filled out in a MIAPPE-compliant way.

* **Workflow RO-Crate Profile**: The existing Workflow RO-Crate profile was updated to support RO-Crate version 1.2 (https://doi.org/10.5281/zenodo.13751027), which was released in June 2025. Once released, this update will enable the Workflow Run Crate profiles and other profiles which build on Workflow RO-Crate to also support RO-Crate 1.2. 

## (4) ISA RO-Crate Export in FAIRDOM-SEEK

Implemented RO-Crate export functionalities in SEEK with ISA profile compliance, establishing the foundation for Investigation-Study-Assay data packaging and validation. 

* Built comprehensive test suite using [ro-crate-ruby](https://github.com/ResearchObject/ro-crate-ruby) gem. 
* JERM ontology types are correctly mapped for ISA entities. 
* Extended Metadata is converted into `schema:PropertyValue` format and embedded in the RO-Crate for each ISA entity.

Parallel work included experimenting with `ro-crate-ruby` to generate assay-level RO-Crates and include extended metadata directly within the crate.

## Validation Strategy Considerations

A key activity was evaluating the different strategies for profile validation. Our goal was to find a method that is not only powerful but also accessible to profile developers who may not be RDF experts.

* **Hand-built SHACL and Python**: The current approach of the `rocrate-validator`, which our project aimed to extend. SHACL is powerful, able to handle complex constraints affecting multiple parts of an RO-Crate, but it has a steep learning curve and can be complex to author and debug. Python is necessary to make assertions about existence of the payload files, because SHACL can only handle the JSON-LD metadata itself.

* **SoSS-based Profiles**: We reviewed a prototype now called RO-Crate MASP (Machine Actionable Schemas and Profiles) [@citesAsRelevant:ro-crate-masp] from the Australian [LDaCA](https://ardc.edu.au/project/language-data-commons-of-australia) team, which proposes extending their existing "Schema.org Style Schema" (SoSS) approach. This aims for a declarative, JSON-LD native method, that could be easier to implement and drive tooling (like editors) directly from the profile. It would also allow profiles to be built interactively using that same RO-Crate tooling. The MASP approach is promising, but is still in early and active development; during the hackathon we found the documentation and examples insufficient to effectively build a new profile. As such, we decided to pursue the SHACL option for immediate development, but may revisit the MASP approach in future once it is more stable. It is theoretically possible to convert between SHACL and the MASP style, as they use a similar conceptual model.

* **LinkML**: Prior investigation by our group at the 2024 BioHackathon explored LinkML as a user-friendly (YAML-based) alternative to generate SHACL [@citesAsAuthority:beier2025biohackeu24]. While promising, this was found to be unviable for now due to significant limitations in the LinkML-to-SHACL generator and in LinkML itself. Key challenges included poor support for RO-Crate patterns like multi-typing (having multiple values for `@type`) and advanced SHACL features (like AND and OR statements) not being supported by the conversion tooling. 

* **Other proposals**: We also noted other proposals in the community, such as [Michael Milton's crate-compatible SHACL profile](https://github.com/WEHI-SODA-Hub/RoCrateProfileProposal?tab=readme-ov-file#proposal)  and [Simon Taurus's JSON-Schema based approach](https://github.com/ResearchObject/ro-crate/issues/442) using the Object Oriented Linked Data Schema (OO-LD) [@citesAsPotentialSolution:oo-ld].

As well as shaping the work in Track 1, this review informed our own profile development (Track 3) and confirmed the need for specialized `PropertyValue` definitions (e.g. for DOIs and PubmedIDs) to improve semantic precision, a feature discussed for the ISA RO-Crate profile.

# Discussion

We successfully defined the architecture for a two-pronged validation system (metadata and data) and made significant progress on the required components.

The data validation track (Frictionless schema conversion) is largely complete. The MIAPPE and ISA profile definitions are well-advanced. The primary remaining tasks are to finalize the `rocrate-validator` extension to use these new profiles and to develop the RO-Crate Profile Crate Creator tool further.

For tabular data validation, the proposed Frictionless-based solution works well and the Docker-based integration into the DataHUB validation framework is working as a proof-of-concept.

DataPLANT maintains a dedicated [registry](https://avpr.nfdi4plants.org) for validation packages - self contained scripts that create a well-defined output that not only create validation reports but can also trigger downstream actions (e.g., sending a JSON payload on badge click) based on the result [@citesAsAuthority:Weil2023].

The logical next step is making Frictionless data validation a first-class citizen in this system, which would mean the extension of the existing .NET script executor to support python as well (to avoid re-writing Frictionless in F# or C#), enabling arbitrary data validation with Frictionless (e.g., data that is not annotated by a Datamap).

A key consideration is that most Python dependency managers do not support single-file scripts with inline dependencies, which is the core feature of F# currently used to make validation packages a single self-contained script (see an example [here](https://avpr.nfdi4plants.org/package/invenio)).
A promising tool for that is [uv](https://docs.astral.sh/uv/guides/scripts/#declaring-script-dependencies), which would enable users to write full validation packages in python.

## Next Steps

Our immediate next steps are:

1. Finalize and publish the ISA and MIAPPE ARC RO-Crate profiles.

2. Complete the extension of the `rocrate-validator` to dynamically load and apply these profiles.

3. Integrate these validation services into DataHUB CI/CD pipelines.

4. Integrate new ISA exporter into FAIRDOM-SEEK’s core, and add ISA profile validation.

This project provides a clear path towards a holistic validation mechanism for ARC RO-Crates, significantly enhancing their FAIRness and reliability.

## Acknowledgements

We thank the organizers of the BioHackathon Europe 2025. This work was funded by ELIXIR, the research infrastructure for life-science data, specifically through the HARVEST project under the Biodiversity, Food Security and Pathogens (BFSP) programme; by the Federal Government of Germany and the county of North Rhine-Westphalia (de.NBI - the German Network for Bioinformatics Infrastructure); by the German Research Foundation (DFG) within the project “Establishment of the National Research Data Infrastructure (NFDI)” in the consortium DataPLANT (https://www.nfdi4plants.de/, project number 442077441) and FAIRagro (www.fairagro.net, project number 501899475); and the European Union through Horizon Europe grant agreement 101058020 (AgroServ) and Horizon 2020 research and innovation programme under grant agreement No. 862613 (AGENT).

We acknowledge the extensive discussions with the members of the Language Data Commons of Australia on machine-actionable profiles and validation strategies.

## References
