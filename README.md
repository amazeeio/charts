# amazee.io Helm Charts

[![Actions Status](https://github.com/amazeeio/charts/workflows/Release%20Charts/badge.svg)](https://github.com/amazeeio/charts/actions)

This repository contains [Helm](https://helm.sh/) charts maintained by [amazee.io](https://amazee.io/).

## Usage

See [here](https://amazeeio.github.io/charts/).

## Contribute

Branch/fork and add/edit a chart in the `charts/` directory.
When you create a PR your change will be automatically linted and tested.
PRs are not mergeable until lint + test passes.

Releases are automatically made for any change which is merged to `main`.

### New charts

Please ensure that any new chart:

* is installable into `kind`, which is used in the CI environment.
  You need a `ci/linter-values.yaml` file with any required dummy values.
  This can be empty if only default values are used.
* has some kind of test, even if it is just a simple connection test.
* has a useful `templates/NOTES.txt`.
* has a `README.md` with some basic information about the chart.

#### Bonus points: well-tuned probes

The CI runs in a [constrained environment](https://docs.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners#supported-runners-and-hardware-resources) which makes it a good place to test how your chart handles slow-starting pods.
Ideally pods should never be killed due to failing probes during chart-install, even if they do eventually start and the chart installation succeeds.
Documentation on probes for pod startup is [here](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes).

## Development tips

### Run chart-testing (lint) locally

```
$ docker run --rm --interactive --detach --network host --name ct "--volume=$(pwd):/workdir" "--workdir=/workdir" --volume=$(pwd)/default.ct.yaml:/etc/ct/ct.yaml quay.io/helmpack/chart-testing:latest cat
$ docker exec ct ct lint
```
