# Python_tools
Repository of python tools

## SNP_density_plot.py
Python script that generates SNP denstisy plots from snpden tabulated files containing SNP stats data output by extract_SNP_info_from_vcf_and_depth.pl Perl script.
It outputs four different types of plots.

![image](https://user-images.githubusercontent.com/76788039/143657829-0c4a0bad-2458-4234-beca-c9ca656c056f.png)

How to run it:

```
usage: SNP_density_plot.py [-h] [-i INPUT] [-o OUTPUT_PREFIX] [-p PLOT_TYPE]

This proram generates SNP-density plots from a SNP density table generated by vcftools

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        SNP density file (snpden)
  -o OUTPUT_PREFIX, --output_prefix OUTPUT_PREFIX
                        output prefix
  -p PLOT_TYPE, --plot_type PLOT_TYPE
                        Plot type [1: snp_density+read-depth; 2: norm_snp_density+read-depth; 3: snp_density+read_coverage; 4: Norm_snp_density+read-
                        depth+read_coverage+median_snp_density_line_per_chr]
```

Example command:

```
python ../scripts/SNP_density_plot.py -i C2_cat.snpden -o C2_cat -p 4
```

Format of a snpden file (columns are separated by TABs):
```
CHROM	    BIN_START	SNP_COUNT	NORM_SNP_COUNT	VARIANTS/KB	DEPTH_MEAN	WINDOW_COV
CP044422	10000	    0	          0	              0.00	     0.7413	      18.35
CP044422	20000	    0	          0	              0.00       0.4529	      11.92
CP044422	30000	    0	          0	              0.00	     0.3768	      12.17
CP044422	40000	    1.00	      6.90	          0.69	     0.5279	      14.49
CP044422	50000	    0	          0	              0.00	     0.4623	      10.44
```
Where:

SNP_COUNT = number of SNPs in a 10 kb window
NORM_SNP_COUNT = number of SNPs in a 10 kb window multiplied by 10000 and divided by the read coverage iin the same window.
VARIANTS/KB = number of SNPs in a 1 kb window
DEPTH_MEAN = mean read depth in a 10 kb window
WINDOW_COV = read coverage percent in a 10 kb window (float 0-100)

*snpden* files can be generated from a VCF file and a depth file output by *samtools depth* tool with the Perl script *extract_SNP_info_from_vcf_and_depth.pl*.

Example command:
```
perl ../scripts/extract_SNP_info_from_vcf_and_depth.pl -b 10000 \
  -d C2_cat.realigned.bam.depth \
  -v NEW_REF_filtered_snps.PASS.C2_cat.FILTER.vcf > C2_cat.snpden
```
