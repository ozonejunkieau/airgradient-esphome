# airgradient-esphome
After seeing Jeff Geerling's [recent video](https://www.youtube.com/watch?v=Cmr5VNALRAg) on the [AirGradient](https://www.airgradient.com/diy/), I wanted one for myself to play with!

Even though the AirGradient team have come up with some great firmware for these devices, I presently run my entire home automation and monitoring platform on NodeRed with MQTT as the backbone, and MQTT isn't supported in the default AirGradient configuration.

I didn't feel like adding this functionality to the firmware, with not enough hours already in the day. Therefore, I created an ESPHome template to enable simple configuration of these devices to report their sensor data over MQTT.

## Configuration
Just copy and paste the `airgradient.yml` file from this repo and add in credentials as required. If you aren't using the display, just remove that code too. If you are unfamilar with the ESPHome process, check out their [pretty good doco](https://esphome.io/guides/getting_started_command_line.html). I believe all the functionality for these devices is in the stable branch, but I am currently running the `dev` branch.

### Font Installation
If you are using the display you will need to download your chosen font (I am using [Open Sans Regular](https://fonts.google.com/specimen/Open+Sans)) and update the `font` section of the file. The display configuration and spacing is set for my font of choice, if you use something different this will need to be updated too.

## Implementation Issues
There seem to be some issues with the CO2 sensor data in ESPHome reporting with invalid data on a regular basis. To get around this I just read the data every second or so and rate limit this in NodeRed prior to writing to InfluxDB. _It's a hack, but it works..._

## Future Plans
* I'd really like to report a single JSON block for either each sensor or for the entire unit, but I've not got that far yet. I may update, or this quick and dirty approach may live on...

* It would also be cool to use the multiple page display stuff to cycle through the different measurements, maybe even including a clock. But that's not going to happen now that this project is deployed and working - let's be honest. Pull requests welcome though!