# Git Policies for RASPBERRY-SI

## Git branching policy
<p align="center">
<img src="./figures/git-policy.png" alt="Git Branching Diagram" width="400">
</p>

This document describes the Git process that the RASPBERRY-SI team follows for development, feature release, and integration testing with the testbeds.
Note that this repository is not intended to contain *all* RASPBERRY-SI code. Other code may exist in different repositories but will be merged into one repository for integration and testing with the testbeds (`OWLAT` and `OceanWATERS`).


There are four permanent branches:

1. **development**: This branch is for internal development and integration
   among different developers and researchers in RASPBERRY-SI. Teams can create feature branches off of this for working changes, new features, etc. For example, if a significant change is warranted, a new feature branch for the change should be created, wherein internal development can proceed. Once the developer is happy with the changes, it should be merged back into development, where it may go through a wider review among the team developing the module/component.

2. **integration-master**: This branch is for code/documentation that is intended for integration staging and testing. For example, if a developer wants to have a new feature reviewed by the PI or NASA, then they should merge from the `development` branch into the `integration-master` branch. The latest version in this branch will be the one required for review. For testbed-specific integration, we use `ow_simulator-integration`, `owlat-sim-integration`, `owlat-physical-integration`. These testbed-specific features will be merged with the `integration-master` branch for integration testing.

3. **master**: This branch is for code/documentation that is intended
   for integration staging and testing before release to the public. 


4. **ow-fixes**: This branch is rebased on the most recent release of 
   `ow_simulator` and is used for facilitating our contribution to the testbeds. If a bug is discovered in `ow_simulator` when working a feature
   branch, cherry-pick the fix into the `ow-fixes` branch and send a pull
   request. We also report the bug in the testbed repositories.


To summarize the intent, if a developer or team wishes to add a feature to
some part of the repository, they should do the following:

1. Create a feature branch from `development` that will contain the development of a new feature.

2. Merge into `development` for internal dev review and unit testing.

3. Merge into `integration-master` for internal integration testing. This branch should always build using a CI.


4. Once integration testing or review is complete, `integration-master` will be merged into `master` and tagged for release to NASA. This will not be done by the developer, but will likely be done by the Autonomy-OW-Integration team.

5. Autonomy-OW-Integration will create a release branch that will contain fixes that might come up during evaluation. At the same time, they will merge these fixes back into `development` and `integration-master` so that problems aren't reintroduced to `master` in subsequent releases.

6. Merge into `master` for public release. `master` is the branch that is used for formal tests and evaluations.
