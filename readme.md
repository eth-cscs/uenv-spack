# uenv-spack

A simplified workflow for using Spack to build software on top of uenv on Alps@CSCS.

```
git clone git@github.com:eth-cscs/uenv-spack.git

# start a uenv with the spack view
uenv start prgenv-gnu/24.11:v1 --view=default,spack

# run the setup script with two arguments
# - the target uarch
# - the path where you want to build your code
./uenv-spack/setup $SCRATCH/work --uarch=gh200
```

Then follow the instructions.

TODO:
* take fingerprint of the input uenv
* add "activation" scripts initialise the environment every time the user wants to use it.
    * it would not take much to convert the view into a uenv `env.json` file, for maximum uenv flexibility
* write docs

Far Future TODO:
* use bwrap to expidite the build process in memory
* pack the result into a squashfs image that can be mounted alongside the uenv
* extend to make creating a python environment from `requirements.txt` etc a doddle.
