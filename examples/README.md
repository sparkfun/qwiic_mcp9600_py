# Sparkfun MCP9600 Examples Reference
Below is a brief summary of each of the example programs included in this repository. To report a bug in any of these examples or to request a new feature or example [submit an issue in our GitHub issues.](https://github.com/sparkfun/qwiic_mcp9600_py/issues). 

NOTE: Any numbering of examples is to retain consistency with the Arduino library from which this was ported. 

## Qwiic Mcp9600 Ex1 Basic
This example outputs the ambient and thermocouple temperatures from the MCP9600 sensor.

## Qwiic Mcp9600 Ex2 Set Type
This example outputs the ambient and thermocouple temperatures from the MCP9600 sensor, but allows for a non
   K-type thermocouple to be used.
   The Qwiic MCP9600 supports K/J/T/N/S/E/B/R type thermocouples, and the type can be configured below!

## Qwiic Mcp9600 Ex3 Set Filter
This example outputs the ambient and thermocouple temperatures from the MCP9600 sensor, but allows the filtering
   onboard the MCP9600 to be controlled. The MCP9600 implements an exponential running average filter, the
   "strength" of which is programmable! The setFilterCoefficient function takes a coefficient between 0 and 7, 
   where 0 disables the filter, 1 corresponds to minimum filtering, and 7 enables maximum filtering. The "strength"
   of the filter just refers to how long it takes for the filter to respond to a step function input. 

   Quick Note! For some reason the getFilterCoefficient() function is a little wierd about returning the proper
   data. This is a known issue and while we've done our best to fix it, every once in a while it might return a 0,
   or the wrong value entirely. We think this is an issue with the MCP9600, and there's not much we can do about it.
   If you'd like to learn more or contact us, check out this issue on GitHub!

   https://github.com/sparkfun/SparkFun_MCP9600_Arduino_Library/issues/1

## Qwiic Mcp9600 Ex4 Set Resolution
This example allows you to change the ADC resolution on the thermocouple (hot) and ambient (cold) junctions. Why
   do this, you ask? Well, setting the resolution lower decreases the sampling time, meaning that you can measure
   high-speed thermal transients! (at the expense of lower resolution, of course).

   Before we start adjusting ADC resolution, a quick word on how this all works. All thermocouple systems have a hot
   and cold junction, and the MCP9600 is no different. Thanks to physics, thermocouples only measure the difference
   in hot and cold junction temperatures, meaning that in order to know the temperature of the hot junction, the
   amplifier needs to know the temperature of cold junction. From there, it will add the cold junction temperature
   to the temperature difference measured by the thermocouple, giving the absolute temperature rather than just the
   relative one.

   This means that the MCP9600 has to take two temperature measurements! Thankfully, the MCP9600 will let us set the 
   resolution on each one independently. SetAmbientResolution and SetThermocoupleResolution configure these measurements
   with a desired resolution for the cold and hot junctions respectively. 

   Cold Junction Possible Resolutions:
   kAmbientResolutionZeroPoint0625   -> Configures the ambient (cold) junction to measure in increments of 0.0625ºC
   kAmbientResolutionZeroPoint25     -> Configures the ambient (cold) junction to measure in increments of 0.25ºC

   Hot Junction Possible Resolutions: 
   kThermocoupleResolution18Bit  -> Reads the hot junction ADC to 18 bits, or 2µV
   kThermocoupleResolution16Bit  -> Reads the hot junction ADC to 16 bits, or 8µV
   kThermocoupleResolution14Bit  -> Reads the hot junction ADC to 14 bits, or 32µV
   kThermocoupleResolution12Bit  -> Reads the hot junction ADC to 12 bits, or 128µV

   It's worth noting that since the thermocouple that serves as the hot junction is arbitrary, we can't provide a 
   specification on how many degrees Celcius precision you will get for a given ADC resolution.

## Qwiic Mcp9600 Ex5 Burst Mode
This example configures the shutdown (or "operating") mode that the MCP9600 runs in. Shutdown mode disables all
   power consuming activities on the MCP9600, including measurements, but it will still respond to I2C commands sent
   over Qwiic. Burst mode is similar, where the MCP9600 is shutdown until the Arduino asks it to wake up and take a 
   number of samples, apply any filtering, update any outputs, and then enter shutdown mode. This example walks
   through that process!

## Qwiic Mcp9600 Ex6 Config Temp Alert
This example outputs the ambient and thermocouple temperatures from the MCP9600 sensor, but allows for a non
   K-type thermocouple to be used.
   The Qwiic MCP9600 supports K/J/T/N/S/E/B/R type thermocouples, and the type can be configured below!


