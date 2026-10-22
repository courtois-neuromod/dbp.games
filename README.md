# dbp.games: PoC recording with datalad-containers

## install


### setup os-level dependencies

This is an approximate command, it depends on the OS and version and whatnot, the idea is to get a functional apptainer and python on the host.

`apt install apptainer python fuse2fs squashfuse gocryptfs`

for instance on Ubuntu 23.10+ it requires setting apparmor profile for apptainer.
```
sudo tee /etc/apparmor.d/apptainer << 'EOF'
# Permit unprivileged user namespace creation for apptainer starter
abi <abi/4.0>,
include <tunables/global>
profile apptainer /usr/{bin/apptainer,libexec/apptainer/bin/starter{,-suid}}
    flags=(unconfined) {
  userns,
  # Site-specific additions and overrides. See local/README for details.
  include if exists <local/apptainer>
}
EOF
```


### setup datalad reqs: can use uv or whatever you prefer.

`pip install datalad git-annex datalad-container`


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
