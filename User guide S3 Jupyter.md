# User Guide S3 and JupyterLab

## S3
Access to the service with the minio_access_key and minio_secret_key provided.
```yaml
# MinIO parameters
# user 20, pass 40
minio_access_key: [ 20 char key ]
minio_secret_key: [ 40 char key ]
```

## Jupyter
### Steps (make venv for a project)

1. Start a terminal session in your JupyterLab server.

2. Make a conda env with a specific path, it could be in a specific project git folder, in this case add it to `.gitignore` file, to not versioning it. You can use `--name` insted of `--prefix` (or `-p`) option of `conda create` to register the venv in `.conda` home user folder.

```bash
conda create -p test
```

3. Activate the conda env and install ipykernel (to auto install deps tree).

```bash
conda activate ./test
conda install ipykernel
```

4. When everything before it is done, without error, then you can register your new (user-project) env to be used to start servers with JupyterHub. For the following command you have to use `sudo` (take care). Reeplace the kernel name, with something refering to (user-project) context. Take care with use the `python` in the `bin` folder of the conda env you have created before.

```bash
sudo test/bin/python -m ipykernel install --prefix=/opt/jupyterhub/ --name 'user-env' --display-name "user-env"
```

5. Restart you JupyterLab server to refresh it. Go to `File` -> `Hub Control Panel` -> `Stop My Server` -(wait some seconds)-> `Start My Server` -> `Launch Server`

6. Check trying to make a new notebook, you have to see a new Kernel with the name you have used.

7. Switch current kernel to your kernel: finally, the you initialize a notebook, by default it will initiate into a default kernel, so last but not least importante it is to switch from that kernel. To do this: `kernel`-> `Change kernel` -> `user-env`. Also, remember that everytime you start/finish a session, you sould activate/deactivate your kernel.

```bash
conda activate ./test
conda deactivate
```

8. (install package step, for future) After this, if you want to install new packages, you have to activate conda and use it to install (or use pip after active conda env)

9. (remove ipykernel, for future) First check kernel list, using `/opt/jupyterhub/bin/jupyter kernelspec list` command, after this (take care you have to use sudo) execute `sudo /opt/jupyterhub/bin/jupyter kernelspec uninstall <name-kernel>` reeplacing `<name-kernel>` with the name of the ipykernel you want to remove. Finally use step 5 to restart server.
