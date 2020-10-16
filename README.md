# Introduction

This repository contains the replication kit for our manuscript [Large-Scale Manual Validation of Bug Fixing Changes: A Fine-grained Analysis of Tangled Changes](LINK MISSING). 

## Contents

- The [Replication-Notebook.ipynb](LINK MISSING) with all code required to reproduce our results from the raw data. 
- The data folder with the hunk_labels.json and the leaderboard.json file. The hunk_labels.json contains the relevant raw data for this study, i.e., the manual labels for the hunks. The leaderboard.json contains daily snapshots of the progress per user and per project. 
- The figures folder with all result figures that are generated by the Replication-Notebook. 

## SmartSHARK MongoDB

The hunk_labels.json only contains the data on hunk level, other information, such as commit messages, issues or similar are not included. The complete data we have for all projects, including the manual labels and the calculated consensus labels is available in [release 1.1 of the SmartSHARK MongoDB](https://smartshark.github.io/dbreleases/). This database is not directly included in this replication kit due to the size, but the database is also available in a [long-term archive on Zenodo](https://doi.org/10.5281/zenodo.4095238). 

## (Optional) Preparing the MongoDB

You need to complete the following steps to prepare you local MongoDB. Please note that most of the replication is possible without the MongoDB, which is why we marked this step as optional. 

- Download a release of the SmartSHARK MongoDB from Zenodo. [You can find a list of releases on our Website](https://smartshark.github.io/dbreleases/). 
- Then, you must prepare the MongoDB instance where you want to host the data. Make sure you install the version that we used for the database backup, which is listed on the Website together with the Link to Zenodo. Otherwise, you may have compability issues. A guide on how to setup a fresh MognoDB can be found [here](https://docs.mongodb.com/manual/installation/#install-mongodb).
- Run [mongorestore](https://docs.mongodb.com/database-tools/mongorestore/) to load the data into your local database.

For example, on Ubuntu 18.04 you can achieve all this as follows for the release 1.1 of our database that we used for this replication kit. 

```
wget -O smartshark_1_1.agz https://zenodo.org/record/4095238/files/smartshark_1_1.agz?download=1
wget -qO - https://www.mongodb.org/static/pgp/server-4.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl daemon-reload
sudo systemctl start mongod
mongorestore --gzip --archive=smartshark_1_1.agz
```

## Running the Notebook

To run our [Replication-Notebook](https://github.com/sherbold/replication-kit-2020-line-validation/blob/main/Replication-Notebook.ipynb), you only need our library [pycoshark](https://github.com/smartshark/pycoSHARK) and [Jupyter Lab](https://jupyter.org/install) (or any other app that can work with Jupyter Notebooks). 

For example, you could run the following commands in your Ubuntu 18.04 machine to get everything running.

```
sudo apt-get install python3-venv build-essential python3-dev
git clone https://github.com/sherbold/replication-kit-2020-line-validation.git
cd replication-kit-2020-line-validation/
python3 -m venv venv
source venv/bin/activate
pip install jupyterlab
jupyter lab
```

You can then open the notebook in your browser and reproduce our results. 


