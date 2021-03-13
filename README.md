# turtlebot3_control
A repo to host Turtlebot3 projects in estimation, mapping, planning, and control.

## Virtual Environment Setup
Setup the virtual environment in order to plot and use the Jupyter Notebooks.

On Ubuntu:
```bash
python3 -m venv tbot-env
source tbot-env/bin/activate
```
On Windows:
```bash
python -m venv tbot-env
.\tbot-env\Scripts\activate
```

### Install Requirements
Once the virtual env is setup and activated, install the supporting modules as below

On Ubuntu:
```bash
pip install --no-cache-dir --upgrade pip
pip install -r ./requirements.txt
jupyter labextension install jupyterlab-plotly
jupyter labextension install @jupyter-widgets/jupyterlab-manager plotlywidget
```
On Windows:
```bash
pip install -r .\requirements.txt
```


## Running
On Ubuntu:
Activate your virtual env if you haven't already done so with
```bash
source tbot-env/bin/activate
```
Then launch the jupyter server with
```bash
jupyter lab
```

On Windows:
Activate your virtual env if you haven't already done so with
```bash
.\tbot-env\Scripts\activate
```
Then launch the jupyter server with
```bash
jupyter notebook
```
