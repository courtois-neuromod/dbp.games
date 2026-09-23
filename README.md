# dbp.games: PoC recording with datalad-containers

## install


### setup os-level dependencies

This is an approximate command, it depends on the OS and version and whatnot, the idea is to get a functional apptainer and python on the host.

`apt install apptainer python`


### setup datalad reqs: can use uv or whatever you prefer.

`pip install datalad git-annex datalad-containers`


`datalad install -s https://github.com/courtois-neuromod/dbp.games`


## run

> this will download the apptainer file the first time

`datalad containers-run -n fmri-gym --  --curriculum curriculums/stk_gym__race.json`


play, exit without error.


## check the records

`git show --name-only`


## Final setup

In the production setup, the repo containing the containers is not the one that will be used to store the collected data.
Another dataset will have this dataset as submodule, effectively tracking the version of the container used to produce the recorded data in the super-dataset.