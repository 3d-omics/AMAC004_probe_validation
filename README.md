# AMAC004_probe_validation
Validation of 16S probes

## Get reads

```sh
cd resources/reads

# D300418 | G069 | TG3 | 28
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300418_1.fq.gz
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300418_2.fq.gz
# D300419 | G084 | TG4 | 14
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300419_1.fq.gz	
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300419_2.fq.gz
# D300422 | G036 | TG2 | 21
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300422_1.fq.gz	
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300422_2.fq.gz
# D300423 | G051 | TG3 | 7
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300423_1.fq.gz	
wget https://sid.erda.dk/share_redirect/BMewg7xQ8c/G_MG/D300423_2.fq.gz
cd ../../
```

## Run pipeline

```sh
# Create screen session
screen -S probe_validation
# screen -r probe_validation #if re-starting the session 

# Load dependencies mamba and snakemake (not needed if they are already installed in root)
module load mamba/1.5.6 snakemake/7.20.0

#Run snakemake
snakemake \
    --use-conda \
    --conda-frontend mamba \
    --rerun-incomplete \
    --jobs 20 \
    --cluster 'sbatch -o logs/{params.jobname}-slurm-%j.out --mem {resources.mem_gb}G --time {resources.time} -c {threads} --job-name={params.jobname} -v'
    --notemp \
    --slurm \
    --latency-wait 600
```
