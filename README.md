# 1000g-megaqc
1000 genomes data processed for use as a MegaQC test set.

## Provenance

### Processing
The data was processed as follows:

* We chose samples from 1000 Genomes Phase 3 that had `*.mapped.ILLUMINA.bwa.*.low_coverage.*.bam` and `*.wgs.COMPLETE_GENOMICS.*.snps_indels_svs_meis.high_coverage.genotypes.vcf.gz` files associated with them
* We then ran these commands over the BAM:
	* `fastqc`
	* `samtools stats --remove-dups --required-flag 1`
	* `mosdepth --no-per-base --fast-mode --by exome.targets.bed`
* On the VCF we ran:
	* `bcftools stats`
* Finally, the data was compiled by running `multiqc stats --module samtools --module bcftools --module fastqc --module mosdepth`

### Tool Versions

* bcftools=1.10.2
* fastqc=0.11.9
* samtools=1.7
* mosdepth=0.2.7
