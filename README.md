# gatk4-HaplotypeCaller-nf
GATK4 HaplotypeCaller step, in gVCF mode, first step for subsequent whole cohort Joint Genotyping, following in GATK [Best Practices](https://software.broadinstitute.org/gatk/best-practices/workflow?id=11145) (step Call Variant Per-Sample).

<img src="https://us.v-cdn.net/5019796/uploads/editor/mz/tzm69d8e2spl.png" width="600" />


## Description

Small, one process pipeline to call recalibrated BAM, on a per sample basis, and store the gVCF. A subsequent pipeline will perform the full cohort calling with all the gVCF files.

## Dependencies 

1. This pipeline is based on [nextflow](https://www.nextflow.io). As we have several nextflow pipelines, we have centralized the common information in the [IARC-nf](https://github.com/IARCbioinfo/IARC-nf) repository. Please read it carefully as it contains essential information for the installation, basic usage and configuration of nextflow and our pipelines.
2. [GATK4 executables](https://software.broadinstitute.org/gatk/download/)

## Input

- `--input` : your intput BAM file(s) (do not forget the quotes for multiple BAM files e.g. `--input "test_*.bam"`)
- `--output_dir` : the folder that will contain your test_123.gVCF file or your test_001.gVCF, test_002.gVCF, ... files.
- `--ref_fasta` : your reference in FASTA. Of course, be sure it is compatible (or the same) with the one that aligned your BAM file(s).
- `--gatk_jar` : the full path to your GATK4 jar file.
- `--interval_list` : not mandatory (for WGS, for example) but recommended (for WES), a file for the intervals to call on. [More information on interval_list format](https://gatkforums.broadinstitute.org/gatk/discussion/1319/collected-faqs-about-interval-lists).

A nextflow.config is also included, modify for suitability outside our pre-configured clusters ([see Nexflow configuration](https://www.nextflow.io/docs/latest/config.html#configuration-file)).

## Usage for Cobalt cluster
```
nextflow run iarcbioinfo/gatk4-HaplotypeCaller.nf -profile cobalt --input "/data/test_*.bam" --output_dir myGVCFs --ref_fasta /ref/Homo_sapiens_assembly38.fasta --gatk_jar /bin/gatk-4.0.4.0/gatk-package-4.0.4.0-local.jar --interval_list target.list
```

