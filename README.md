# ESM-VFC stacks

![env-create](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/env-create/badge.svg)
![env-create-maint](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/env-create-maint/badge.svg)
![repo2docker](https://github.com/ESM-VFC/esm-vfc-stacks/workflows/repo2docker/badge.svg)

Central compute environment definition(s) for ESM VFC.

## How to use?

### Just use the environment file

You can just use the [env file](environment-esm-vfc.yml) to install everything with Conda.

Note, however, that this env file does not specify any of the Jupyter and Dask configs that we also set in this repo.

### Use the pre-built Docker images with _Docker_

You can use [docker images](https://hub.docker.com/r/esmvfc/esm-vfc-stacks) that come with a fully working (repo2docker-built) Jupyter environment and run them with docker.

Assuming you want to expose your work directory to `/work` in the container, and run:
```shell
docker pull esmvfc/esm-vfc-stacks:latest
docker run \
    -v ${HOME}/work/:/work -w /work \
    -p 8888:8888 esmvfc/esm-vfc-stacks:latest \
    jupyter lab --no-browser --ip="0.0.0.0" --port="8888"
```
If you want to run a specific version of this image, replace the tag `latest` accordingly.
All available versions [are found on Dockerhub](https://hub.docker.com/r/esmvfc/esm-vfc-stacks/tags).


### Use the pre-built Docker images with _Singularity_

To run from your `work/` dir with Singularity:
```shell
cd ${HOME}/work/
singularity run \
    -B $(mktemp -d):/run/user \
    docker://esmvfc/esm-vfc-stacks:<tag> \
    jupyer lab --no-browser --ip="0.0.0.0"
```

If you want to run a specific version of this image, replace the tag `latest` accordingly.
All available versions [are found on Dockerhub](https://hub.docker.com/r/esmvfc/esm-vfc-stacks/tags).


## How to contribute?

Modify the [env file](environment-esm-vfc.yml) or any of the [Binder config](.binder/) or [Dask config](.dask/) with a pull request.

## Releases

There are no Github-based releases.
Instead, we use [calver](https://calver.org/) to build whenever something is pushed to `master` and tag it as `YYYY.MM.DD-<Git SHA>` on [dockerhub](https://hub.docker.com/r/esmvfc/esm-vfc-stacks).
