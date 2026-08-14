# Analysis results

Outputs from `ipk2026_metagenomics_arg_pipeline.ga`, run on three samples from the inlet of the
Lynetten wastewater treatment plant, Copenhagen (PRJEB79372). Each file is named
`step<NN>_<SAMPLE>_<what it is>`, so it can be traced back to a step in the `.ga` without guessing,
and each sample has its own directory so a file stays identifiable when it is pulled out on its own.

## Samples

| Directory | Run | Collected |
| --- | --- | --- |
| `CPH1042` | ERR13597805 | September 2022 |
| `CPH1025` | ERR13597803 | October 2022 |
| `CPH1051` | ERR13597804 | January 2023 |

Every numbered output below exists three times, once per sample. Sizes are the range across the
three.

## Files

| Prefix | Workflow step | Tool as configured | What it holds | Size | In the release |
| --- | --- | --- | --- | --- | --- |
| `step03` | 3, Kraken2 | PlusPF 2022-06-07, confidence 0.1 | Full taxonomic report, one row per taxon. The first row is the unclassified fraction | 0.7 to 1.0 MB | yes |
| `step04` | 4, Bracken | Species level, threshold 10 reads | Re-estimated species abundances | 0.1 to 0.3 MB | yes |
| `step05` | 5, Krona | From the Bracken report | Interactive composition chart, opens in a browser | 0.6 to 1.2 MB | yes |
| `step07` | 7, MEGAHIT | meta-large settings, minimum contig 500 bp | The assembly | 117 to 229 MB | no |
| `step08` | 8, ABRicate, Branch B | CARD, minimum identity 80 | Every alignment: gene, contig, coverage, identity, resistance class | 9 to 16 KB | yes |
| `step11` | 11, ABRicate Summary | Across the sample's reports | Gene by sample presence table | under 1 KB | yes |
| `step12` | 12, Alpha diversity | Shannon, from Bracken | One number per sample | under 1 KB | yes |
| `step13` | 13, Beta diversity | Bray-Curtis, from Bracken | Pairwise dissimilarity | under 1 KB | yes |
| `step14` | 14, antiSMASH | MIBiG comparison on, ClusterBlast off | Full HTML report plus the per-cluster GenBank files | 8.7 to 15 MB | yes |
| `step15` | 15, BiG-SCAPE | Cutoff 0.3, on the sample's own clusters | Gene cluster family network, HTML | 3.7 to 4.6 MB | yes |
| `step19` | 19, Transpose | Branch B summary | Gene names in column 1, ready to join | under 1 KB | yes |
| `step21` | 21, CARD ARO Normalize | CARD ARO gene family mapping | Branch B collapsed to families. Header line carries `NUM_FOUND` | 1 to 2 KB | yes |
| `step27` | 27, GROOT | ARG-ANNOT, window 150, `--lowCov` | Branch A raw calls, ARG-ANNOT nomenclature | under 1 KB | yes |
| `step28` | 28, CARD Family Normalize | argNorm chained with CARD aro_index | Branch A in the same vocabulary as Branch B | under 1 KB | yes |
| `step29` | 29, Branch A vs B | Join, unmatched only | Families the reads found and the assembly did not | under 1 KB | yes |
| `step30` | 30, Branch A vs B | Join, unmatched only, reverse | Families the assembly found and the reads did not | 1 KB | yes |
| `step33` | 33, Zero-hit guard | awk | The summary after the empty-result case is made safe | under 1 KB | yes |
| `step37` | 37, Pre-filter contigs | awk, length at least 1 kb | The subset antiSMASH sees | 52 to 114 MB | no |
| `step38` | 38, DeepARG | LS model, minimum probability 0.8, alignment identity 50 | `_deeparg_ARG` (p at or above 0.8) and `_deeparg_potential_ARG` (p below 0.8) | 11 to 28 KB | yes |
| `step39` | 39, Candidate contigs | Filter by ID, on the Potential ARG contig IDs | Whole contigs for every candidate, with the neighbourhood attached | 134 to 567 KB | yes |
| `step40` | 40, Dedupe Branch B | awk, by CARD family | One row per family | under 1 KB | yes |
| `step41` | 41, Dedupe Branch A | awk, by CARD family | One row per family | under 1 KB | yes |

Unprefixed files in each sample directory are provenance rather than pipeline output: `ids.json`
holds the Galaxy dataset identifiers and `history_contents.json` the history dump.

## downstream/

Local follow-up performed after the workflow, so these files carry no step number: the detected ARG
proteins and their nucleotide sequences, the whole contigs they sit on, remote BLAST results and
NCBI lookups for the best hits, the PyMOL superposition of the predicted structures against their
references, and the two scripts that draw the site map and the Venn diagram.

## Attribution

Some of what is in here is derived from reference data that carries its own terms. Credit is
required in every case, and one of them restricts commercial use.

### CARD

`card_gene_family_map.tsv`, the `NUM_FOUND` normalisation in `step21`, `step28`, `step40` and
`step41`, and the `PRODUCT` and `ACCESSION` fields of every ABRicate report are derived from the
Comprehensive Antibiotic Resistance Database, curated at McMaster University. The ontology files
CARD publishes, which include `aro_index.tsv`, are released under CC BY 4.0; the rest of CARD is
free for academic, government and non-profit use and requires written permission from McMaster
University for commercial use. Anyone reusing these files commercially should go to CARD rather
than assume this archive settles the question.

> Alcock BP, Huynh W, Chalil R, et al. CARD 2023: expanded curation, support for machine learning,
> and resistome prediction at the Comprehensive Antibiotic Resistance Database. Nucleic Acids Res.
> 2023;51(D1):D690-9. doi:10.1093/nar/gkac920

### AlphaFold Protein Structure Database

`downstream/structures/TETW_ref_AF.pdb` and `TET39_ref_AF.pdb` were downloaded from AlphaFold DB
and are used under CC BY 4.0. The other 25 structures in that directory were predicted here with
ESMFold from the sequences the pipeline recovered.

> Varadi M, Bertoni D, Magana P, et al. AlphaFold Protein Structure Database in 2024: providing
> structure coverage for over 214 million protein sequences. Nucleic Acids Res. 2024;52(D1):D368-75.
> doi:10.1093/nar/gkad1011
>
> Jumper J, Evans R, Pritzel A, et al. Highly accurate protein structure prediction with AlphaFold.
> Nature. 2021;596(7873):583-9. doi:10.1038/s41586-021-03819-2
>
> Lin Z, Akin H, Rao R, et al. Evolutionary-scale prediction of atomic-level protein structure with
> a language model. Science. 2023;379(6637):1123-30. doi:10.1126/science.ade2574

### ARG-ANNOT and argNorm

Branch A calls names its genes in ARG-ANNOT's vocabulary. The table that translates those names
into CARD gene families is chained from argNorm's published `groot_ARO_mapping.tsv`
(github.com/BigDataBiology/argNorm, MIT) and CARD's `aro_index.tsv`.

> Gupta SK, Padmanabhan BR, Diene SM, et al. ARG-ANNOT, a new bioinformatic tool to discover
> antibiotic resistance genes in bacterial genomes. Antimicrob Agents Chemother. 2014;58(1):212-20.
> doi:10.1128/AAC.01310-13

### Map tiles

`downstream/make_map.py` draws its basemap from CartoDB Positron tiles at run time. Any image it
produces has to carry "Basemap © OpenStreetMap contributors © CARTO", which the script writes into
the figure itself. The tiles are not redistributed here.

## Distribution

The two assembly steps account for 700 MB of the 777 MB here and exceed GitHub's 100 MB per-file
limit. They are derived data: anyone can regenerate them from the run accession and the workflow
file, which is what distributing a `.ga` is for. Everything else totals 58 MB and ships as one
compressed archive attached to a release.
