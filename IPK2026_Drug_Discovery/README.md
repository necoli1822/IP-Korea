# Metagenome-based Understanding and Exploiting Resistance Genes for New Drug Targets

Materials for the **Metagenomics (ARL)** session, Day 4 of the IPK 2026 course
*Mastering the Art of Drug Discovery: Technologies, Tools, and Applications*.
Thursday 27 August 2026, 90 minutes. Antibiotic Resistance Laboratory, Institut Pasteur Korea.

## Abstract

Antimicrobial resistance was directly responsible for an estimated 1.27 million deaths in 2019 and contributed to nearly five million more, and the projection for 2050 is worse on both counts. The conventional answer, to discover the next antibiotic, has been failing for two reasons that compound each other. Scientifically, target-based screening produced potent compounds that could not cross the Gram-negative outer membrane, so the bottleneck turned out to be accumulation rather than affinity. Commercially, an antibiotic is punished for working: the course is short, the patient is cured, and stewardship then asks that the best new agent be used as little as possible.

This session argues that the more tractable move is upstream. Resistance is carried by genes rather than by organisms, and those genes travel on plasmids, integrons and transposons between species that no culture plate would ever present side by side. If the transmissible unit is the gene, the unit of surveillance has to be the gene pool rather than the isolate, and that pool is invisible to culture and only partly visible to genotype-based prediction. The lecture builds this case by first defining what an antibiotic is and what a clinical breakpoint actually claims, then showing where both definitions fail: an MIC quantifies how much drug is needed, never how long nor for what fraction of the population, which is precisely where tolerance, persistence and heteroresistance operate.

The demonstration applies that argument to real data. A Galaxy workflow is run on metagenomes from the inlet of the Lynetten wastewater treatment plant in Copenhagen, roughly three kilometres downstream of a vancomycin manufacturing site, so that the selection pressure is a property of the location rather than an inference from the result. The workflow profiles the community, assembles it, detects known resistance genes against CARD, and then relaxes the identity threshold with a machine-learning classifier to surface genes that carry resistance-like signal but match no described family. The recovered resistome includes a complete *vanA* operon, and the low-confidence tier contains the candidates the session exists to produce.

Those candidates are the handover. A gene with no known family is exactly the case in which sequence homology has nothing further to say, which is where structure prediction, docking and molecular dynamics take over, and where cheminformatics asks what chemical space could occupy the site. Sequence identity is where this session stops, and structure is where the next one starts.

## Programme

| Day | Date | Theme | Sessions |
| --- | --- | --- | --- |
| 1 | Mon 24 Aug 2026 | Introduction to Drug Discovery: essentials for drug discovery (assay development, cell painting) | The drug discovery pipeline, from target identification to clinical trials; key challenges and strategies in early drug discovery<br>Production of reproducible cell material and quality assessment<br>Assay development and optimisation for cell-based assays<br>Assay development and functional genomics<br>*Practical training:* assay development and screening |
| 2 | Tue 25 Aug 2026 | Advanced Screening Technologies and Automation for Drug Discovery | Advanced screening technologies: morphological profiling and translational assay systems<br>Organoids and 3D systems<br>Overview of available HCS instrumentation<br>*Practical training:* HCS instrumentation technologies<br>Sample management and automation<br>*Practical training:* liquid handling and automation |
| 3 | Wed 26 Aug 2026 | Image Processing and Hit-to-Lead Optimisation (Chemistry) | Overview of image analysis using Harmony software<br>*Practical training:* using image analysis software<br>Chemistry for biologists and chemical diversity used for screening *(IP Lille)*<br>Hit-to-lead optimisation, target identification, HCS versus target-based assays *(IP Lille)*<br>Natural products, libraries, small molecules, extracts *(IP Montevideo)* |
| **4** | **Thu 27 Aug 2026** | **Innovative Tools for Drug Discovery: Leveraging AI and Bioinformatics** | Transcriptomics *(IP Montevideo)*<br>**Metagenomics *(ARL)*** <br>Managing and mining chemical and assay data<br>*Practical training:* data curation for integrated database and visualisation; virtual screening<br>Deep learning for image analysis |
| 5 | Fri 28 Aug 2026 | Case Study and Presentation | Case study: deep dive into the Q203 drug discovery process, from early target identification to clinical application<br>Participants' presentations |

## Contents of this directory

To follow:

- [ ] `ipk2026_metagenomics_arg_pipeline.ga`, the Galaxy workflow used in the demonstration
- [ ] Session README: how to import and run the workflow on usegalaxy.eu
- [ ] Screen captures from the demonstration run

Pipeline outputs are not committed to this directory. They are published as a single compressed
archive attached to a release, which keeps them out of the repository history. Assemblies are
excluded from that archive as well: they are reproducible from the run accession and the workflow
file.
