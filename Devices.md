# Devices contained in the dataset

## BeeWi Motion Sensor

- Dataset ID: beeWiMotion
- Model: BSMOT-EUR rev. AW11
- BDADDR: 04:A3:16:67:20:A9
- Control: `OtioHome` app
- Actions:
  - Data = App running, caused a motion detection
  - ColdData = Start the app, cause a motion detection, close the app
  - ExpandedData = App running, select the motion sensor widget, cause a motion detection
- Advertising:
  - Intermittent pattern, dual advertising interval
  - Advertising interval: 1060 ms
  - After connection:
    - Duration: 8 s
    - Advertising interval: 200 ms
- Notes:
    - ColdData in clean environment is ExpandedData in office (The app wasn't able to start within a minute, so a detailed view was used instead.)
    - Sample ExpandedData 3 is missing
    - Some samples affected by two errors:
      - Motion sensor was triggered during office/expandedData sample (office/expandedData 1, 4, 5)
      - Brownout during boot caused timing offset for one channel

## Bentech FP3

- Dataset ID: bentech
- Model: FP3
- BDADDR: DC:23:4F:A9:9A:46
- Control: `Tuya` app
  - Application keeps an open connection (no advertisements in non-cold actions)
- Actions:
  - Lock = App running, lock the smart lock (manually)
  - Unlock = App running, unlock the smart lock in the app
  - ColdLock = Start the app, lock the smart lock (manually), close the app
  - ColdUnlock = Start the app, unlock the smart lock in the app, close the app
- Advertising:
  - Intermittent pattern
  - Advertising interval: 1003 ms
- Notes:
  - Sample office/ColdUnlock 3 failed to capture the connection

## Danalock

- Dataset ID: danalock
- Model: Danalock V3-BTZE
- BDADDR: E8:15:D4:F5:BA:BA
- Control: `Danalock` app
  - There are multiple apps available:
    - Danalock Classic (official, original app)
    - Danalock (official, since fall 2023)
    - smartlock.de Danalock App (unofficial)
- Actions:
  - Lock = App running, lock the smart lock in the app
  - Unlock = App running, unlock the smart lock in the app
  - ColdLock = Start the app, lock the smart lock in the app, close the app
  - ColdUnlock = Start the app, unlock the smart lock in the app, close the app
- Advertising:
  - Intermittent pattern
  - Advertising interval: 500 ms
- Notes:
  - Activity Log is not kept on the device and displaying the log does not trigger a Bluetooth communication.
  - Some samples are affected by errors: 
    - Parallel/office - ColdLock 1, 2, 3; Lock 3, 4, 5, Unlock 2
      - Probably a brownout during boot caused ESP monitoring channel 39 to reboot, which caused the timestamps to be skewed. This renders the mixed data unusable as the connection is hidden by the skew.

## Philips Hue white

- Dataset ID: hueBulb
- Model: 9290018216
- BDADDR: FF:CB:D1:DC:DF:EA
- Control: `Philips Hue` app
- Actions:
  - On = App running, switch the bulb on with the widget
  - Off = App running, switch the bulb off with the widget
  - ColdOn = Start the app, switch the bulb on with the widget, close the app
  - ColdOff = Start the app, switch the bulb off with the widget, close the app
  - ConfigOn = App running, open the config (click on the widget), switch the bulb on, go back to overview
  - ConfigOff = App running, open the config (click on the widget), switch the bulb off, go back to overview
  - Luminance = App running, open the config (click on the widget), change the luminance level, go back to overview
  - Effect = App running, open the config (click on the widget), select the effect, go back to overview
- Advertising:
  - Persistent pattern
  - Advertising interval: 856 ms

## Philips Hue Smart plug

- Dataset ID: huePlug
- Model: 9290018216
- BDADDR: D7:3F:2B:21:A4:63
- Control: `Philips Hue` app
- Actions:
  - On = App running, switch the plug on with the widget
  - Off = App running, switch the plug off with the widget
  - ColdOn = Start the app, switch the plug on with the widget, close the app
  - ColdOff = Start the app, switch the plug off with the widget, close the app
- Advertising:
  - Persistent pattern
  - Advertising interval: 327 ms
- Notes:
  - In shielded room, the advertising interval exhibits a strange pattern with alternating between 300 ms and 350 ms instead of random jitter around one advertising interval.

## igloohome Padlock Lite

- Dataset ID: igloohome
- Model: SP3B
- BDADDR: CB:94:54:ED:5D:28
- Control: `igloohome` app
- Actions:
  - Lock = App running, lock the smart lock in the app
  - Unlock = App running, unlock the smart lock in the app
  - ColdLock = Start the app, lock the smart lock in the app, close the app
  - ColdUnlock = Start the app, unlock the smart lock in the app, close the app
  - Log = App running, go to lock details > Logs tab and click the "Get recent logs"
- Advertising:
  - Persistent pattern
  - Advertising interval: 414 ms
- Notes:
  - Parallel/Office/Passive 3 contains strange last advertising packet (on channel 38) with timestamp 17 minutes after the last-but-one.
  - Both collectors detect a strange cluster of advertising packets in the beginning of the Unlock 1 and 3 samples in the shielded room.

## Mi Temperature and Huminity Monitor 2

- Dataset ID: miTemp
- Model: LYWSD03MMC
- BDADDR: A4:C1:38:E0:67:AE
- Control: `Mi Home` app
- Actions:
  - Data = App running, select the "Temperature & humidity" widget, wait until the data is loaded (including the history graph), go back to the app home screen
  - ColdData = Start the app, select the "Temperature & humidity" widget, wait until the data is loaded (including the history graph), close the app.
- Advertising:
  - Intermittent pattern
  - Advertising interval: 2191 ms
- Notes:
  - Samples office/ColdData 4, 5 failed to capture the connection and are too short
  - Some samples captured by the parallel collector have too low advertising deltas for the first advertising packet:
    - In the shielded room affected samples are: All ColdData, Data 1,2,4,5, Passive 1,2,4
    - In the office affected samples are: ColdData 3, Data 3, Passive 1

## Nuki Smart Lock

- Dataset ID: nuki
- Model: Nuki Smart Lock 3.0
- Type: 010.318
- BDADDR: 54:D2:72:64:1B:F4
- Control: `Nuki Smart Lock` app
- Actions:
  - Lock = App running, lock the smart lock in the app
  - Unlock = App running, unlock the smart lock in the app
  - ColdLock = Start the app, lock the smart lock in the app, close the app
  - ColdUnlock = Start the app, unlock the smart lock in the app, close the app
  - Log = App running, go to lock settings in the app and display the activity log
- Advertising:
  - Persistent pattern, dual advertising interval
  - Advertising interval: 1010
  - After connection:
    - Duration: 4 s
    - Advertising interval: 44 ms
- Notes:
  - Log action does not trigger the faster advertising
  - Some samples are affected by errors: 
    - Parallel/clean - ColdLock 5, ColdUnlock 5
      - Probably a brownout during boot caused ESP monitoring channel 39 to reboot, which caused the timestamps to be skewed. This renders the mixed data unusable as the connection is hidden by the skew.

## Revogi Bluetooth LED bulb

- Dataset ID: revogi
- Model: LTB012
- BDADDR: E0:E5:CF:15:17:48
- Control: `DeLite` app
  - Application keeps an open connection (no advertisements in non-cold actions)
- Actions:
  - On = App running, switch the bulb on in the list of connected devices
  - Off = App running, switch the bulb off in the list of connected devices
  - ColdOn = Start the app, switch the bulb on in the list of connected devices, close the app
  - ColdOff = Start the app, switch the bulb off in the list of connected devices, close the app
  - ConfigOn = App running, select the bulb in the list of connected devices, switch the bulb on, go back to the list of connected devices
  - ConfigOff = App running, select the bulb in the list of connected devices, switch the bulb off, go back to the list of connected devices
  - Luminance = App running, select the bulb in the list of connected devices, change the luminance level, go back to the list of connected devices
  - Effect = App running, select the bulb in the list of connected devices, select the effect, go back to the list of connected devices
  - Colour = App running, select the bulb in the list of connected devices, change the hue, go back to the list of connected devices
- Advertising:
  - Intermittent pattern
  - Advertising interval: 55 ms
- Notes:
  - In Passive captures the parallel collector detected an exceptionally high advertising delay which is not visible with the controller collector. The delay is present in the following samples:
    - Office/passive 1 - all channels
    - Office/passive 3 - all channels
    - Office/passive 4 - channels 37,38
    - Office/passive 5 - channel 38
