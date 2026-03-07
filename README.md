# WiMAP WiFi Access Point Localization using RSSI

This project implements the **WiMAP (Where is My Access Point)** algorithm for estimating the location of a WiFi Access Point using **Received Signal Strength Indicator (RSSI)** measurements.

The implementation is based on the research paper:

"WiMAP: an Efficient Wi-Fi Access Point Localization Mechanism"  
Presented at the International Computer Sciences and Informatics Conference (ICSIC).

---

## Project Overview

Wireless localization is an important technique used in indoor navigation, wireless network optimization, and security analysis.

The WiMAP algorithm estimates the location of a WiFi Access Point by:

1. Collecting RSSI measurements at known locations
2. Filtering the strongest signal measurements
3. Applying a centroid-based localization method

Compared with traditional centroid-based approaches, WiMAP improves localization accuracy by **ignoring weak signal samples that introduce positioning errors**.

---

# 1. RSSI Sample Collection

The first step was to collect RSSI measurements at different locations inside the room.  
For each measurement point, the following parameters were recorded:

- RSSI (Received Signal Strength Indicator)
- Data transfer rate (Mbps)
- Distance from the Access Point (meters)
- \(10 \times \log_{10}(d)\) used in the path-loss calculation

RSSI Samples pic

A total of **15 measurement points** were collected across the room.

---

# 2. Mapping the Measurement Points

After collecting the samples, the measurement points were plotted on the room layout according to their coordinates using AutoCAD.

This step helps visualize the distribution of the collected RSSI samples.

Room Mapping pic

Each point represents a location where RSSI measurements were taken.

---

# 3. Path Loss Model Estimation

Using the collected RSSI data, a regression model was used to estimate the indoor path loss model.

RSSI = -2.48 (10 log10(d)) - 35.6

Where:

- d = distance from the access point
- n = 2.48 (estimated propagation exponent)
- RSSI at 1 meter = -35.6 dBm

This model helps describe how signal strength decreases with distance.

Path Loss Model pic

---

# 4. WiMAP Localization

The WiMAP algorithm estimates the Access Point location using the following steps:

1. Sort RSSI samples by signal strength
2. Select the strongest 20% of samples
3. Compute the centroid of those locations

Centroid calculation:

x_AP = (Σ xi) / N  
y_AP = (Σ yi) / N

Where N is the number of selected sample points.

---

# 5. Estimated Access Point Location

Using the strongest RSSI samples, the estimated Access Point position was calculated.

Estimated Coordinates:

X = 406.30  
Y = 668.51

The estimated AP position is shown in the figure below.

Estimated AP Location pic

Due to the limited dataset (15 samples), the estimated location deviates from the true AP position. Increasing the number of samples would improve localization accuracy.

---
