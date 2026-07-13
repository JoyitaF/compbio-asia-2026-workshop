# 7. Sequence Annotation

**Source:** `0616-CompBioAsia2026_annotation.pptx`  
**Date indicated by filename:** 16 June 2026.

The sequence-annotation session explained how we go from raw sequence data to biological meaning. The central question was: once we have a genome or metagenome assembly, how do we identify genes and infer what they do?

Important teachings:

- Bacterial and eukaryotic genomes have different annotation challenges.
- ORFs can be detected using start/stop codons, but longest ORF is only a heuristic.
- Introns, repeats, pseudogenes, and alternative splicing complicate eukaryotic annotation.
- Metagenomic assembly is harder because reads come from mixed organisms.
- Binning can group contigs into MAGs, but MAGs are still reconstructed approximations.
- Functional annotation often uses enzyme families, KEGG, KOfam, and pathway databases.
- Transposable elements are mobile DNA sequences; they complicate assembly and gene prediction.

The teaching was useful beyond genomics because it showed a recurring computational biology theme: raw data is not knowledge. Each annotation step makes assumptions, and those assumptions need validation.

See also: [`lectures/07-sequence-annotation.md`](lectures/07-sequence-annotation.md)
