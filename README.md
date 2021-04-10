# Conda-Build Dojo

**/ˈdōˌjō/**<br>
*noun*<br>
a hall or place for immersive learning or meditation.

*Conda-Build Dojo* walks you through lessons that re-create scenarios encountered during package building.

## TODO

- Show all lessons (in curriculum.yaml)
- Show my history.
- Add color to the prompt (use colorama).
- Clean up.
- Lesons to add:
    - Create a patch (including on GitHub!)
    - Port a patch
    - Oniguruma (upstream breaking change)

## Design
- The learner makes their own fork of this repo and clones it on target platforms.
- Snapshots in time:
    - Packages in Repo: Download needed packages into local directory and run "conda index" to pretend they're channels.
    - Recipes in AnacondaRecipes: commits
- Run `dojo` and follow objectives and steps to complete lessons.

## Development

1. Clone this repo to your local machine.
1. Spin up the `c3i_linux-64` docker image, mounted to a path that can reach your clone of the repo and `aggregate`.
1. From this repo's root directory, create the conda environment.
```
conda env create --file env.yaml
```
1. Activate the conda environment.
```
conda activate dojo_dev
```
1. Install this repo in dev mode.
```
pip install -e .
```

## Platforms

### Linux

1. Fork this repo to your personal Github account.
1. Clone this repo locally (e.g. on your Mac).
1. Run the `c3i_linux-64` Docker image to spin up a container, mounted to a path that can reach your clone of the repo and `aggregate`.
1. `cd` to this repo, and install it in dev mode (`pip install . -e`)
1. Run `dojo`.

### OSX

(TBD)

### Windows

(TBD)

## How to create a lesson

1. Run:
```
dojo create_lesson --name <LESSON_NAME>
```
1. Fill out the `lesson.yaml`.
1. If your lesson requires `dojo_channels` (e.g. fake channels that recreate the channel conditions for your lesson), create and populate a `dojo_channels_pkgs.txt` file in the lesson directory.
    - Create an env with your target package installed in it. Make sure to include all build, host run, and test requirements. This will capture the FULL list of packages you need to build your target package in dojo.
    - Run: `conda list -n test_env --explicit`
    - Copy and paste the list of URLs into `dojo_channel_pkgs.txt`
        - Delete any URLs for the packages that should be removed for the lesson (i.e. the packages that the learner is expected to build).
