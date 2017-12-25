# Jupyter Notebook:  Getting Started
The Jupyter notebook is an interactive computational environment, in which you can combine code, execution, rich text, mathematics, plots and rich media. 

---

### [Install the Notebook](http://jupyter.readthedocs.io/en/latest/install.html)
Installing Jupyter using Anaconda and conda:  
For new users, we highly recommend [installing Anaconda](https://www.continuum.io/downloads). Anaconda conveniently installs Python, the Jupyter Notebook, and other commonly used packages for scientific computing and data science.  (Prereq: Python is installed.)

Once anaconda is installed, you can launch the notebook by typing
```{bash}
$ jupyter notebook
```

### Upgrade all libraries/packages
We will now update all the packages/libraries installed by anaconda to ensure you have the latest version of everything!

```{bash}
$ conda update --all
```

### Run the Notebook at Terminal Prompt  
Note:  The notebook will open at the directory in which you launch the notebook on your terminal.  
```
$ jupyter notebook
```
>my example
```console
vladimirlazovskiy$ jupyter notebook
[I 01:58:38.085 NotebookApp] JupyterLab alpha preview extension loaded from /Users/vladimirlazovskiy/anaconda3/lib/python3.6/site-packages/jupyterlab
[I 01:58:38.085 NotebookApp] JupyterLab application directory is /Users/vladimirlazovskiy/anaconda3/share/jupyter/lab
[I 01:58:38.092 NotebookApp] Serving notebooks from local directory: /Users/vladimirlazovskiy
[I 01:58:38.093 NotebookApp] 0 active kernels
[I 01:58:38.093 NotebookApp] The Jupyter Notebook is running at:
[I 01:58:38.093 NotebookApp] http://localhost:8888/?token=7830d216798b0838ee3ce02eb5f51ffea5e7c4ba45d2f332
[I 01:58:38.093 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 01:58:38.096 NotebookApp] 
    
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=7830d216798b0838ee3ce02eb5f51ffea5e7c4ba45d2f332
[I 01:58:38.229 NotebookApp] Accepting one-time-token-authenticated connection from ::1
```

### Shut Down the Juypter Notebook App
At terminal prompt:  
 * control + c
 * type:  `y`
 
>my example 
```console
^C[I 02:00:51.309 NotebookApp] interrupted
Serving notebooks from local directory: /Users/vladimirlazovskiy
0 active kernels
The Jupyter Notebook is running at:
http://localhost:8888/?token=7830d216798b0838ee3ce02eb5f51ffea5e7c4ba45d2f332
Shutdown this notebook server (y/[n])? y
[C 02:00:53.087 NotebookApp] Shutdown confirmed
[I 02:00:53.088 NotebookApp] Shutting down 0 kernels
vladimirlazovskiy$ 
```

---

### Getting to Know Jupyter

You can try out Jupyter on a browser without installing it.  
https://try.jupyter.org/

