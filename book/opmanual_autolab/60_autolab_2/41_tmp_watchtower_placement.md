# Placing Watchtowers {#autolab-2-watchtower-placement status=draft}

<div class='requirements' markdown="1">

Requires: Assembled [Watchtowers](#watchtower-hardware).

Results: A Watchtower system ready to be used.

</div>

<minitoc/>

Note: If you have a RPi4, the command for flashing the SD card is (`XX` is a number starting from 01):

    laptop $ dts init_sd_card --country ![two_letter_country_code] --hostname ![watchtowerXX] --type watchtower --configuration WT21A


Refer to the [Watchtowers](#watchtower-hardware) section for how to build a watchtower.

## Placement of the watchtowers

This is a picture of the current Autolab in ETHZ. It will give you a quick approximate of how to place your watchtowers and how many you should put.

<div figure-id="fig:tmp_autolab_picture">
<img src="opmanual_autolab/images/watchtower_placement/autolab_image.jpg" style="width: 90%"/>
<figcaption>
Picture of the Zurich ETH Autolab.
</figcaption>
</div>

There's only two general rule of putting Watchtowers in a city. 

- First, make sure that the field of views of Watchtowers do cover the whole city. 
- Second, there should be enough overlapping between field of view between Watchtowers.

Below is a more synthetic view of the watchtower placement in ETHZ. The ratio of watchtower to road tiles is around 2/3.

<div figure-id="fig:tmp_watchtower_placement">
<img src="opmanual_autolab/images/watchtower_placement/autolab_wt_placement.png" style="width: 60%"/>
<figcaption>
Overview of the autolab and of the watchtower placement. Each number shows the position of a watchtower. Watchtowers number 01 to 16 are on the left loop, while watchtower 21 to 35 are on the right loop.
</figcaption>
</div>

Below is the field of view of watchtowers. Please keep in mind that they cover approximately 3 tiles each (even more in some cases), but that on the edge of the image, despite rectification, the image is distorted and thus the apriltag detection might give inaccurate results. This is why overlapping field of view are important. The more the better. 

<div figure-id="fig:tmp_watchtower_view_corner">
<img src="opmanual_autolab/images/watchtower_placement/wt_view_corner.png" style="width: 90%"/>
<figcaption>
View from a watchtower in a corner. It covers approximately 3 tiles.
</figcaption>
</div>

<div figure-id="fig:tmp_watchtower_view_straight_line">
<img src="opmanual_autolab/images/watchtower_placement/wt_view_straight.png" style="width: 90%"/>
<figcaption>
View from a watchtower on a straight line. It covers approximately 3 tiles.
</figcaption>
</div>

## Connection of the watchtowers

Beside the placement of Watchtowers, they should be connected via ethernet cables. At ETH, the Watchtowers are first connected to switches, that are connected to our router. At ETHZ, all of the Autolab is on a stage, and we pull the cables directly from underneath it, to keep the track clean from cables.

Then we have one PC connected via ethernet to the router, for faster and more reliable communication with the watchtowers.

### Recommended network setup

Since all Watchtowers might send data at the same time, we recommend you have a strong network setup:

The best, and currently used in the ETHZ Autolab, is a switch with 1 Gb/s ports for each watchtower, with 2 ports at 10 Gb/s, that are connected to a central computer (which in turn needs a 10 Gb/s network card).

Todo: explain the router requirements.

### Power management

Last but not least, these Watchtowers needs _power_. Remember to prepare your USB chargers and cables that support 2.4A output.

Note: EXPERIMENTAL : If you want to get less cables around, the possibility of using POE (power over ethernet) exists. With a additional hat, you can power the pi directly by the ethernet cable (provided that you switch provides the service as well).
