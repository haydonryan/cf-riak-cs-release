# riak-release

A BOSH release for Riak and Riak CS.

Make sure to run `git submodule update --init` before creating the release.

This project is based on [BrianMMcClain/riak-release](https://github.com/BrianMMcClain/riak-release).

## Deploying to [BOSH lite]

After you create and upload the release:

1. Put your director UUID into `templates/riak-cs-service.yml`
2. Generate the manifest: `./generate_deployment_manifest warden > riak-cs-service.yml`
3. `bosh deployment riak-cs-service.yml && bosh deploy`

## Caveats

We have not tested changing the structure of a live cluster, e.g. changing the seed node.

## Blobs

Instructions for creating the blobs for this release.
For each blob you want to update:

1. Remove its entry from `config/blobs.yml`
2. Remove the cached blob from `.blobs/` (you can find it by checking the symlink in `blobs/<package>/`)
3. Copy the new blob into `blobs/<package>/`
4. Upload the new blob: `bosh upload blobs`

### riak

Clone the [riak repository](https://github.com/basho/riak), check out the desired tag, and `make dist`.
The resulting `tar.gz` file can be found in the working directory.

### riak-cs

Clone the [riak_cs repository](https://github.com/basho/riak_cs), check out the desired tag, and `make package.src`.
The resulting `tar.gz` file can be found in the `package/` directory.

### stanchion

Clone the [stanchion repository](https://github.com/basho/stanchion), check out the desired tag, and `make package.src`.
The resulting `tar.gz` file can be found in the `package/` directory.

### other

TODO - verify where the `git`, and `erlang` tarfiles came from.

## TODO

- The settings for the Riak job in this release are configured with options suggested by Basho for deploying Riak in a Riak CS cluster.  We could add an option to configure Riak for standalone operation (when a manifest includes only Riak but not Riak CS) 

[BOSH lite]: https://github.com/cloudfoundry/bosh-lite
