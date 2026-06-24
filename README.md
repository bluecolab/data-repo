# data-repo

Depository for flat data files. From the sensors individual origins (2018) to 2025.

## Stations

### Locations

Please note that GPS locations are only available historically (a few years back) only for Ada, Alan, and Odin via the API.

#### Alan

| Type | Latitude            | Longitude          |
| ---- | ------------------- | ------------------ |
| DD   | 41.1277363000700406 | -73.80833696495597 |
| DMSN | 41° 7' 39.851'' N   | 73° 48' 30.013'' W |

#### Ada

| Type | Latitude            | Longitude          |
| ---- | ------------------- | ------------------ |
| DD   | 41.1277363000700406 | -73.80833696495597 |
| DMSN | 41° 7' 39.851'' N   | 73° 48' 30.013'' W |

#### Odin

| Type | Latitude           | Longitude          |
| ---- | ------------------ | ------------------ |
| DD   | 41.127019099325075 | -73.80846521250481 |
| DMSN | 41° 7' 37.269'' N  | 73° 48' 30.474'' W |

#### Njord

| Type | Latitude | Longitude  |
| ---- | -------- | ---------- |
| DD   | 41.1308  | -73.810165 |

#### Skadi

| Type | Latitude  | Longitude |
| ---- | --------- | --------- |
| DD   | 41.124355 | -73.80812 |

## Sensors

Each station reports a fixed set of sensor channels. The column headers in the CSV files correspond to the sensor IDs listed below. Authoritative sensor names, IDs, and descriptions can also be retrieved directly from the Blue CoLab API endpoints — the units below reflect the standard configuration for these instruments and should be confirmed against the API, since some channels can be reported in alternate units.

Ada and Alan are water-quality sondes and share the same channel set. Odin is a weather station. PurpleAir measures air quality.

#### Ada & Alan — Water Quality

| Sensor | Measures                      | Units               | Significance                                                                                                                        |
| ------ | ----------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Temp   | Water temperature             | °C                  | Drives dissolved-oxygen capacity, reaction rates, and habitat suitability; the baseline reading that contextualizes all the others. |
| pH     | Acidity / alkalinity          | pH (0–14, unitless) | How acidic or basic the water is; affects aquatic life and the solubility of metals and nutrients.                                  |
| Cond   | Specific conductance          | µS/cm               | Proxy for dissolved-ion content (salts, minerals); sudden jumps can signal pollution or road-salt runoff.                           |
| DOpct  | Dissolved oxygen (saturation) | % saturation        | Oxygen available to aquatic life relative to saturation; low values stress or kill fish and invertebrates.                          |
| Sal    | Salinity                      | PSU                 | Dissolved salt content; in a freshwater stream, elevated salinity often flags road-salt influence or intrusion.                     |
| Turb   | Turbidity                     | NTU                 | Water cloudiness from suspended particles; spikes follow storms, erosion, or disturbance and reduce light and habitat quality.      |

#### Odin — Weather

| Sensor           | Measures                           | Units           | Significance                                                       |
| ---------------- | ---------------------------------- | --------------- | ------------------------------------------------------------------ |
| AirTemp          | Air temperature                    | °C              | Ambient air temperature at the station.                            |
| BaroPressure     | Barometric pressure                | hPa             | Atmospheric pressure; falling pressure often precedes storms.      |
| RelHumid         | Relative humidity                  | %               | Air moisture relative to saturation.                               |
| RelHumidTemp     | Temperature at the humidity sensor | °C              | Sensor-body temperature used in deriving relative humidity.        |
| VaporPressure    | Water-vapor partial pressure       | hPa             | Amount of water vapor in the air; relates humidity to temperature. |
| WindSpeed        | Wind speed (average)               | m/s             | Average wind speed over the interval.                              |
| MaxWindSpeed     | Wind speed (peak gust)             | m/s             | Strongest gust recorded during the interval.                       |
| WindDir          | Wind direction                     | degrees (0–360) | Compass direction the wind originates from.                        |
| Rain             | Precipitation                      | mm              | Rainfall accumulated over the interval.                            |
| SolarFlux        | Solar irradiance                   | W/m²            | Instantaneous incoming solar radiation.                            |
| SolarTotalFlux   | Total solar radiation              | W/m²            | Accumulated solar energy over the interval.                        |
| LightningStrikes | Lightning strike count             | count           | Number of strikes detected in the interval.                        |
| DistLightning    | Distance to lightning              | km              | Estimated distance to detected strikes.                            |
| TiltNS           | Station tilt, north–south axis     | degrees         | Leveling/orientation diagnostic for the station mount.             |
| TiltWE           | Station tilt, west–east axis       | degrees         | Leveling/orientation diagnostic for the station mount.             |

#### PurpleAir — Air Quality

| Sensor      | Measures                                                     | Units | Significance                                                                                  |
| ----------- | ------------------------------------------------------------ | ----- | --------------------------------------------------------------------------------------------- |
| pm2.5_atm   | Fine particulate matter (≤2.5 µm), "atmospheric" calibration | µg/m³ | Outdoor-tuned PM2.5 estimate; the standard reading for ambient air quality and health impact. |
| pm2.5_cf_1  | Fine particulate matter (≤2.5 µm), CF=1 calibration          | µg/m³ | Indoor/high-concentration-tuned PM2.5 estimate; reads higher than the atmospheric variant.    |
| humidity    | Relative humidity                                            | %     | Humidity at the sensor; influences particulate readings and is used in corrections.           |
| temperature | Air temperature                                              | °F    | Internal temperature of the sensor. Often reads higher then outside temperature.              |
| pressure    | Barometric pressure                                          | hPa   | Atmospheric pressure at the sensor.                                                           |

**Notes**

- Ada and Alan's source system carries additional water-quality channels that have not been historically collected
- Ada and Odin data prior to the March 2022 migration originates from the older MariaDB system; data from March 2022 onward comes from the TimescaleDB/PostgreSQL system. Columns have been standardized across both sources so each station's yearly files share an identical layout.
- GPS coordinates (lat/lon) are available historically (a few years back) for Ada, Alan, and Odin only. The lat/lon for PurpleAir are not via GPS and manually entered by Justin.
