- /store/empa/apps/stacks/
    - /prgenv-gnu-24.11      uenv e.g. prgenv-gnu/24.11:v1
        - /spack            git clone github:spack/spack
        - /store
        - /cache
        - /config
            - meta.json
            - /system
            - /user
        - activate


        - /envs
            - /gpaw
                - activate.sh
            - /cp2k-fancy-atoms

```
uenv start prgenv-gnu/24.11 --view=spack
uenv-spack --uarch=gh200 --specs="libxc,libvdwxc,py-gpaw" /dev/shm/bcumming/gpaw
```

# create the top level path with spack, store, cache etc that will be _shared_ by all envs
uenv start prgenv-gnu/24.11 --view=spack
uenv-spack setup --uarch=gh200 /store/empa/apps/stacks/prgenv-gnu-24.11

uenv-spack setup --uarch=gh200 --uenv=prgenv-gnu/24.11 /store/empa/apps/stacks/prgenv-gnu-24.11

# create an env inside a top level path
uenv-spack env /store/empa/apps/stacks/prgenv-gnu-24.11 gpaw --specs="py-gpaw,libxc"
uenv-spack env /store/empa/apps/stacks/prgenv-gnu-24.11 gpaw --recipe=$SCRATCH/empa-spack/recipes/gpaw

# detect from current directory as default
cd /store/empa/apps/stacks/prgenv-gnu-24.11
uenv-spack env gpaw --recipe=$SCRATCH/empa-spack/recipes/gpaw
uenv-spack env --stack=$PWD --recipe=$SCRATCH/empa-spack/recipes/gpaw gpaw
uenv-spack env --stack=/store/empa/apps/stacks/prgenv-gnu-24.11 --recipe=$SCRATCH/empa-spack/recipes/gpaw gpaw

# detect from the activated stack
cd /store/empa/apps/stacks/prgenv-gnu-24.11
source activate
activate gpaw
