## Process of Pipeline communicating between IRIDA and Galaxy
Overall: 
1. IRIDA sends the details of the pipeline to Galaxy
2. Galaxy receives the details and submits the jobs to SLURM
3. Once the job is done, galaxy returns the results to IRIDA

## 

At Galaxy VM to find where "galaxy workflow are stored": 
```
> find . -name "*.ga"
```
There are no .ga files found.
