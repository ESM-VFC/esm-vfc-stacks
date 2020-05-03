# ESM-VFC stacks

![env-create](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/env-create/badge.svg)
![env-create-maint](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/env-create-maint/badge.svg)
![repo2docker](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/repo2docker/badge.svg)

Central compute environment definition(s) for ESM VFC.

## How to use?

You can just use the [env file](environment-esm-vfc.yml) to install everything with Conda.

You can use [docker images](https://hub.docker.com/r/esmvfc/esm-vfc-stacks) that come with a fully working (repo2docker-built) Jupyter environment and run them with docker. Assuming you want to expose your work directory to `/work` in the container, and run:
```shell
docker run \
    -v ${HOME}/work/:/work -w /work \
    -p 8888:8888 esmvfc/esm-vfc-stacks:<tag> \
    jupyter lab --no-browser --ip="0.0.0.0" --port="8888"
```
To run from your `work/` dir with Singularity:
```shell
cd ${HOME}/work/
singularity run \
    -B $(mktemp -d):/run/user \
    docker://esmvfc/esm-vfc-stacks:<tag> \
    jupyer lab --no-browser --ip="0.0.0.0"
```

## How to contribute?

Modify the [env file](environment-esm-vfc.yml) with a pull request.

## Releases

There are no Github-based releases.
Instead, we use [calver](https://calver.org/) to build whenever something is pushed to `master` and tag it as `YYYY.MM.DD-<Git SHA>` on [dockerhub](https://hub.docker.com/r/esmvfc/esm-vfc-stacks).
