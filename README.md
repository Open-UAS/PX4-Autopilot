# PX4 Drone Autopilot, OpenUAS Fork

## ***Switch to the [stable branch](https://github.com/LTL-AERO/PX4-Autopilot/tree/stable)***

**The default branch (master) is only used for repository management and documentation, it does not contain any source code**


## Steps to compile custom firmware for Gazebo simulation

**Gazebo simulation is only supported on linux**

 1) Clone forked px4 repository to your machine `git clone --branch stable https://github.com/LTL-AERO/PX4-Autopilot.git`
 2) Run `git submodule update --init --recursive` to clone all submodules within the repository, to your machine
     - alternatively `git submodule update --init --recursive <submodule folder>` can be used if you know the specific submodule needed 
     - `git submodule update --recursive` can be run in the future to update all submodules
 3) Follow [this guide](https://dev.px4.io/master/en/setup/dev_env_linux.html) to setup your development environment
     - The provided scripts by default also download the firmware to `~/src/firmware`, this can be deleted
 4) Attempt to build the [simulation target](https://dev.px4.io/master/en/simulation/gazebo.html#running-the-simulation) of the firmware by running `make px4_sitl gazebo_plane` from within the firmware folder
     - You may need to install additional libraries, these are the ones that work for my system
        <details>
            <summary>Libraries</summary>
             
             sudo apt install python3-pip
             pip3 install --user empy
             pip3 install --user pyros-genmsg
             pip3 install --user packaging
             pip3 install --user toml
             pip3 install --user numpy

             sudo apt install libgstreamer1.0-dev
             sudo apt install gstreamer1.0-plugins-good
             sudo apt install gstreamer1.0-plugins-bad
             sudo apt install gstreamer1.0-plugins-ugly

             sudo apt install gstreamer1.0-libav gstreamer1.0-gl
      </details>
 5) To run the simulation with the OpenUAS model use `make px4_sitl gazebo_open_uas`
 6) Open QGroundControl to connect to and control the simulation
 
 - additional details on running gazebo simulations with the px4 [can be found here](https://dev.px4.io/master/en/simulation/gazebo.html#gazebo-simulation)


## Airframe documentation

This fork adds several airframes that are developed by the OpenUAS team, they are as follows,

1) 2150_open_uas
    - Simulation airframe
    - Made for gazebo simulations
    - Fixed wing, standard plane
    - config file: /ROMFS/px4fmu_common/init.d-posix/2150_open_uas
2) 2151_open_uas_apprentice
    - Airframe for the Apprentice off the shelf plane
    - contains custom defualt configurations specific to the Apprentice
    - Fixed wing, standard plane
    - config file: /ROMFS/px4fmu_common/init.d/airframes/2151_open_uas_apprentice

## Repo Structure

The github repository is managed by the [wei/Pull app](https://github.com/wei/pull) ([config file](.github/pull.yml)) and a submodule [update script](.github/workflows/update_submodules.yml)

The stable branch is where development will be done on. The stable branch is only updated on the official PX4 repo when a new version of the PX4 firmware is released (about once a month). Working on this branch reduces the possible issues that would appear from developing on a frequently changing branch.

'Pull' will monitor the official PX4 repo, when the official stable branch is updated (a new release is published), 'Pull' will create a pull request to merge the changes from the official stable branch into our stable branch. This pull request will almost certainly have conflicts and will need to be resolved before the new version can be merged into our stable branch. Using an IDE is recommended for resolving merge conflicts.

The config file for 'Pull' and the submodule update script must be on the default branch (master). These are placed in a separate branch from main development to prevent accidental deletion when the stable branch is updated from upstream.


## Other Resources

- [useful link for making a new airframe](https://discuss.px4.io/t/create-custom-model-for-sitl/6700/3)
- A good explication of git submodules: [Git Submodules: Adding, Using, Removing, Updating](https://chrisjean.com/git-submodules-adding-using-removing-and-updating/)
