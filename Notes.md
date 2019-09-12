Quickstart
------------

1. gcloud command-line tool (https://cloud.google.com/pubsub/docs/quickstart-cli)
1. Install Conda and Jupyter on gpu-blue-controller
1. Create a *notebook.sh* on gpu-blue-controller with the following content
```
#!/bin/bash
#SBATCH --nodes 1
#SBATCH --ntasks-per-node 1
#SBATCH --gres=gpu:2
#SBATCH --mem-per-cpu=4G
#SBATCH --time 1-0:00:00
#SBATCH --job-name jupyter-notebook
#SBATCH --output jupyter-notebook-%J.log

jupyter notebook --ip=0.0.0.0
```
1. Start a notebook instance
```
gcloud compute ssh gpu-blue-controller --command 'sbatch notebook.sh'
```
1. Get the name of the notebook instance, e.g. gpu-blue-compute4 (on gpu-blue-controller).
```
squeue -j [jobid]
```
1. Once the instance is in running (R) state, forward the Jupyter's port to local.
```
gcloud compute  ssh --ssh-flag="-L 8888:gpu-blue-compute4:8888" gpu-blue-controller
```
1. Access Jupyter from local browser on http://localhost:8888 
