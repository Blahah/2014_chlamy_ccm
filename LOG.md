## Data downloaded from BGI

## Analyse with fastqc
```
cp ~/data/chlamy/cdts.genomics.hk/Raw_data/*gz . && \
mkdir fastqc && \
fastqc *.fq.gz --threads 8 --outdir fastqc
```

## Trim adapters with Trimmomatic

## Run eXpress on all samples

used script at: https://gist.github.com/Blahah/9a22945529633b36a6f6/c5b5967638674885e4304b438d30eb83ff3b8297

```bash
rds45@node8:/tmp/rds45$ ./express.rb --reads trimmed.csv --fasta Creinhardtii_281_v5.5.transcript.fa --path express --output express_summary.txt -k 10
```
