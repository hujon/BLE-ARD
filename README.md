# Bluetooth Low Energy - Advertising Records Dataset

This dataset is designed to provide a comprehensive view of the advertising behavior of selected devices, 
enabling detailed analysis of their communication patterns.

The dataset comprises 1020 samples, each capturing one minute of advertising report occurrences from various Bluetooth-enabled devices.
Each record within a sample includes key data points such as Timestamp, Bluetooth Address, Address Type, Advertising Type, and RSSI (Received Signal Strength Indicator).

## Collectors

Data collection was facilitated using two different collectors:
- controller: A Cypress CYW43455 BLE controller integrated within a Raspberry Pi 3B+.
- parallel: A custom-built probe equipped with three Espressif ESP32-WROOM-32E chipsets, each dedicated to monitoring a separate advertising channel.

The records from the `parallel` collector contain also Channel on which the advertising was received and Device Name, if available.

## Devices

The devices monitored encompass a range of functionalities, categorized into four types:
- Locks:
  - Bentech FP3
  - Danalock V3-BTZE
  - igloohome Padlock Lite
  - Nuki Smart Lock 3.0
- Lighting:
  - Philips Hue white
  - Revogi Bluetooth LED bulb
- Actuators:
  - Philips Hue Smart plug
- Sensors:
  - Mi Temperature and Humidity Monitor 2
  - BeeWi Motion Sensor

## Environments

The measurements were carried out in two different environments:
- clean: A shielded chamber containing only one (measured) device at any time, the control device and our monitoring probe, in order to achieve the cleanest possible results.
- office: Typical office environment, which included several other Bluetooth devices and a WiFi access point, to accurately represent common operating conditions.

## Structure of the dataset

Three process steps are included in the dataset to enable faster work with the dataset.
- capture: raw data from the advertisement collectors (CSV files with the advertisement metadata)
- cleaned: the capture data without duplicities and ordered by time (parallel collector)
- filtered: the clean data filtered to always contain only the monitored device advertisement information

The structure then follow the pattern:

- Process step
  - Collector
    - Environment
        - Device
          - Sample
