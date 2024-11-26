# Sensit.App.Automate
The Automated Test App (Sensit.App.Automate) can control a variety of equipment and send commands at intervals chosen by the user.  Its best use is for controlling lab equipment such as mass flow controllers, power supplies, etc. for automated tests (hence the name).  Results are stored in a CSV file.

The calibration app defines a test as a series of _devices_, which are equipment such as mass flow controllers and power supplies, and _events_, which are commands sent to a device.

# Example
Suppose we want to test a carbon monoxide sensor to see how accurate it is.  For this, we need to mix carbon monoxide and air in various quantities .  We'll use two mass flow meters; one for air and the other for carbon monoxide.  If we have a bottle of normal air, and a bottle of 100 ppm carbon monoxide, we might do a test where we apply 0, 50, and 100 ppm carbon monoxide at 300 sccm to our sensor for 3 minutes each and record its response.

To set up this test, you'll need to have two [Alicat MC-Series Mass Flow Controllers](https://www.alicat.com/models/mc-series-gas-mass-flow-controllers/).  Alternatively, there is a device called "Simulator" that can be used if you'd like to just see the program running and make a sample logfile.

To set up this test in the automated test app, define the following devices in the "Devices" tab:
* a mass flow controller called "Carbon Monoxide"
* a mass flow controller called "Air"

Once the devices are defined, select a serial port for each device.  The app automatically populates a dropdown control with all the serial ports available on the computer.

Then define the following events in the "Events" tab:
* Set **_Air_** mass flow to **_300 sccm_** for **_180 seconds_**.
* Set **_Carbon Monoxide_** mass flow to **_150 sccm_** for **_0 seconds_**.
* Set **_Air_** mass flow to **_150 sccm_** for **_180 seconds_**.
* Set **_Carbon Monoxide_** mass flow to **_300 sccm_** for **_0 seconds_**.
* Set **_Air_** mass flow to **_0 sccm_** for **_180 seconds_**.

Note that the duration of each event is how long the program should wait before executing the next event, so events that should happen at the same time (such as setting mass flow on multiple devices) have a duration of 0 seconds.

To save this test so it can be used again in the future, click _File -> Save As_.

On the "Log" tab, click Browse to select a filename.  This will be a CSV file with data from the mass flow controllers.

If we wanted the test to repeat over and over (until stopped manually), we could set enable **_Repeat_**.  For this example, we'll leave it set on **_No_**, which means the events will only execute once.

Finally, click "Start", then wait for the test to complete.