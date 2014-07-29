## Data downloaded from BGI

## Analyse with fastqc
```
cp ~/data/chlamy/cdts.genomics.hk/Raw_data/*gz . && \
mkdir fastqc && \
fastqc *.fq.gz --threads 8 --outdir fastqc
```

## Trim adapters with Trimmomatic

`reads.txt`:
```
140710_I607_FCC4TB2ACXX_L1_Index12_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index12_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index13_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index13_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index14_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index14_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index15_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index15_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index16_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index16_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index18_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index18_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index19_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index19_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index2_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index2_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index4_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index4_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index5_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index5_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index6_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index6_2.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index7_1.fq.gz
140710_I607_FCC4TB2ACXX_L1_Index7_2.fq.gz
```

run trimmomatic...

```bash
$ ./trim/trim-batch.rb --pairedfile reads.txt --jar /applications/trimmomatic/Trimmomatic-0.32/trimmomatic-0.32.jar --adapters /applications/trimmomatic/Trimmomatic-0.32/trimmomatic-0.32.jar --threads 16 --phred 64 | tee trim2.log
```

reads2.txt for files that need to be re-run:

```
140710_I607_FCC4TB2ACXX_L1_Index7_1.fq
140710_I607_FCC4TB2ACXX_L1_Index7_2.fq
140710_I607_FCC4TB2ACXX_L1_Index12_1.fq
140710_I607_FCC4TB2ACXX_L1_Index12_2.fq
```

re-run for missing files:

```bash
$ ./trim/trim-batch.rb --pairedfile reads2.txt --jar /applications/trimmomatic/Trimmomatic-0.32/trimmomatic-0.32.jar --adapters /applications/trimmomatic/Trimmomatic-0.32/trimmomatic-0.32.jar --threads 16 --phred 64 | tee trim2.log
```

## Run eXpress on all samples

used script at: https://gist.github.com/Blahah/9a22945529633b36a6f6/c5b5967638674885e4304b438d30eb83ff3b8297

trimmed.csv (for now we don't group samples or conditions:

```
trim/t.140710_I607_FCC4TB2ACXX_L1_Index12_1.fq,1,1,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index12_2.fq,1,1,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index12_1.fq,1,1,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index12_2.fq,1,1,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index13_1.fq,1,2,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index13_2.fq,1,2,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index13_1.fq,1,2,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index13_2.fq,1,2,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index14_1.fq,1,3,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index14_2.fq,1,3,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index14_1.fq,1,3,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index14_2.fq,1,3,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index15_1.fq,1,4,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index15_2.fq,1,4,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index15_1.fq,1,4,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index15_2.fq,1,4,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index16_1.fq,1,5,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index16_2.fq,1,5,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index16_1.fq,1,5,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index16_2.fq,1,5,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index18_1.fq,1,6,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index18_2.fq,1,6,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index18_1.fq,1,6,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index18_2.fq,1,6,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index19_1.fq,1,7,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index19_2.fq,1,7,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index19_1.fq,1,7,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index19_2.fq,1,7,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index2_1.fq,1,8,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index2_2.fq,1,8,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index2_1.fq,1,8,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index2_2.fq,1,8,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index4_1.fq,1,9,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index4_2.fq,1,9,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index4_1.fq,1,9,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index4_2.fq,1,9,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index5_1.fq,1,10,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index5_2.fq,1,10,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index5_1.fq,1,10,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index5_2.fq,1,10,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index6_1.fq,1,11,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index6_2.fq,1,11,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index6_1.fq,1,11,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index6_2.fq,1,11,3
trim/t.140710_I607_FCC4TB2ACXX_L1_Index7_1.fq,1,12,1
trim/t.140710_I607_FCC4TB2ACXX_L1_Index7_2.fq,1,12,2
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index7_1.fq,1,12,3
trim/^tu.140710_I607_FCC4TB2ACXX_L1_Index7_2.fq,1,12,3
```

```bash
$ ./express.rb --reads trimmed.csv --fasta Creinhardtii_281_v5.5.transcript.fa --path express --output express_summary.txt -k 10
```
