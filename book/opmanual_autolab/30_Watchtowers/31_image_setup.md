# Watchtower Initialization {#watchtower-initialization status=ready}

<div class='requirements' markdown="1">

Requires: An SD card of size at least 32 GB.

Requires: A computer with a **Ubuntu OS** (for flashing the SD card), an internet connection, an SD card reader, and 16 GB of free space.

Requires: Duckietown Shell, Docker, etc, as configured in [](+opmanual_duckiebot#laptop-setup).

Requires: Duckietown Token set up as in [](+opmanual_duckiebot#dt-account).


Results: A ready watchtower

Next Steps: [Place the Watchtower in the city](#localization-watchtower-placement).
</div>

## Flashing the SD card

The image setup procedure for Watchtowers is the same as for Duckiebots.

Warning: If you are a host for AIDO compeition and you are setting up watchtower, you must follow the following instructions.

**Naming Convention:** (By default when flashing the SD card)

* --linux-username: **duckie** 
* --linux-password: **quackquack**
* hostname: **watchtowerXX** (where XX specify the number of the Watchtower)

Note: As of 2020 October, the option for user to set the username and password has been removed. User should not set the username and password manually.

**Changable options:** 

* --wifi: sets the wifi refer [here](+opmanual_duckiebot#setup-duckiebot) for more instruction. **If you are using watchtower in an autolab, this should not be set.** 
* --configuration: sets the configuration. Currently supports WT18, WT19A, WT19B.
* --no-cache: this ensures to use the latest image available.

**Example Fashing command:**

A complete command will look like:

    laptop $ dts init_sd_card --hostname watchtower![XX] --country ![COUNTRY] --type watchtower --configuration WT19B

Using the above naming conventions, you can flash your SD cards as is described in [Duckiebot Initialization](+opmanual_duckiebot#setup-duckiebot).

## Calibrating the camera

Using the instruction in [](+opmanual_duckiebot#camera-calib), you should do only the intrinsic calibration for the Watchtowers.

Note: Be sure to check the quality of the image. It should be (1296x972) and not (480*640) like on the Autobots. If it is not, this means you didnt flash the Watchtower with the `--type watchtower` argument. To solve this, reflash it.
