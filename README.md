# AMAC004_probe_validation
Validation of 16S probes

```sh
# Load dependencies mamba and snakemake (not needed if they are already installed in root)
module load mamba/1.5.6 snakemake/7.20.0

screen -r probe_validation

#Run snakemake
snakemake \
    --use-conda \
    --conda-frontend mamba \
    --rerun-incomplete \
    --jobs 20 \
    --cluster 'sbatch -o logs/{params.jobname}-slurm-%j.out --mem {resources.mem_gb}G --time {resources.time} -c {threads} --job-name={params.jobname} -v'
    --keep-going \
    --notemp \
    --slurm \
    --latency-wait 60
```
