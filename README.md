# Guided-wave dataset

## 1. Overview
This dataset contains ultrasonic guided-wave measurements from a water-filled pipe, acquired under flow and no-flow conditions at different water temperatures, for an undamaged pipe and three cumulative damage stages.
Guided waves are widely used for structural health monitoring of pipelines because they can inspect long lengths of pipe from a single transducer location. In practice, however, the guided-wave response is affected by many factors besides damage. Internal fluid flow and temperature changes alter wave propagation, heating changes the properties and dimensions of the pipe, and the coupling of the transducers to the surface can vary with temperature and over time. These effects change the recorded signals and can mask, or be mistaken for, the changes caused by damage, which makes reliable damage detection difficult.
This dataset was collected to study damage detection under such conditions. It includes internal water flow, water temperatures from room temperature up to 55 °C, and three cumulative damage stages (two notches and a surface pit) on the same pipe, so flow, temperature and damage effects are all present in the measurements. Torsional guided-wave modes were used for excitation and sensing, and signals were recorded with a ring of 16 PZT transducers. The data can be used to develop and test damage detection, localisation and compensation methods under near-realistic operating conditions.

Contact: [Sheetal Patil, patilsheetal2697@gmail.com, ORCID: https://orcid.org/0009-0002-2768-1152]
Corresponding author: [Prof. Siddharth Tallur, stallur@iitb.ac.in]

## 2. Test specimen
- Pipe material: Steel
- Outer diameter: 57.3 mm
- Wall thickness: 4 mm
- Length: 1000 mm

## 3. Sensors and acquisition

  ### 3.1 Transducers
  - Type: shear-mode piezoelectric plates (d15) from APC International (American Piezo), https://www.americanpiezo.com. Product datasheet: https://americanpiezo.com/wp-content/uploads/2023/11/apc_70-50xx.pdf
  - Material: APC 850
  - Dimensions: 15 mm x 15 mm x 1 mm
  - Number and layout: 16 transducers (PZT1 to PZT16), attached equidistantly around the pipe circumference at 22.5° spacing (e.g., PZT3 = 45°, PZT5 = 90°, PZT14 = 292.5°). Channel `chN` in the data files corresponds to PZT N.
  - Distances along the pipe are measured from the transducer ring.
  - Excitation: T(0,1) Torsional guided-wave modes 

  ### 3.2 Data acquisition
  - Instrument: custom-built FPGA-based acquisition system using a PYNQ-Z2 board
  - Excitation signal: Hann-windowed toneburst with 5 and 7 cycles 
  - Excitation frequencies: 50, 55, 60, 65, 70 and 75 kHz (stage D3 only: 50, 60 and 70 kHz)
  - Sampling rate: 2 MHz (time step 0.5 µs)
  - Record length: 8187 samples (about 4.09 ms) per channel
  - Units of recorded signals: Volts

## 4. Damage stages (cumulative, same pipe)
| Stage | Folder | Defects present |
|---|---|---|
| D0 | `D0_baseline` | none (undamaged) |
| D1 | `D1_notch` | N1 |
| D2 | `D2_notch_notch` | N1, N2 |
| D3 | `D3_notch_notch_pit` | N1, N2, P1 |

| ID | Type | Location | Distance from ring | Axial | Circumferential | Depth |
|---|---|---|---|---|---|---|
| N1 | Notch | Along axis of PZT3 (45°) | 700 mm | 4 mm | 30 mm | 2 mm |
| N2 | Notch | Along axis of PZT5 (90°) | 500 mm | 4 mm | 30 mm | 2 mm |
| P1 | Surface pit | Along axis of PZT14 (292.5°) | 800 mm | 18 mm | 15 mm | 2 mm |

All defects were made with a Dremel rotary tool. Dimensions are approximate.

## 5. Test conditions
- **Flow:** water flowing through the pipe (`flow`) or no water (`noflow`). Flow rate: 0.5m/s.
- **Temperature:** room temperature (`Troom`, at ambient laboratory temperature), and 40, 45, 50 and 55 °C (`T40C` to `T55C`). Water was heated with two immersion heaters and continuously circulated.
- No-flow data at 55 °C were not collected.
- **Repeats:** each condition has `run01` and `run02`. Stage D3 has `run01` only. Only the first two runs per condition are included in this dataset.

## 6. Folder structure
```
D#_stage/
  flow/ or noflow/
    Troom/, T40C/, T45C/, T50C/, T55C/
      run01/, run02/
        f<freq>k_5c.csv, f<freq>k_7c.csv, f<freq>k_10c.csv
```
Each damage stage is provided as a separate zip file.

## 7. File format
Files are named `f<frequency>k_<cycles>c.csv`, where the frequency is in kHz, e.g., `f50k_7c.csv` is the 50 kHz, 7-cycle Hann-windowed excitation. Files for 5 and 7 cycles are in the same run folder.

Each file has a header row and 17 columns: `time` (s), then `ch1` to `ch16` (signal from PZT1 to PZT16, in [V]). One row per sample.

## 8. Metadata files (`metadata/`)
- `experiment_log.csv`: one row per run (damage stage, flow, water temperature, run number, folder path). Each listed run folder contains the 5, 7 and 10-cycle files.
- `damage_description.csv`: location and size of each defect.
- `damage_stages.csv`: which defects are present in each stage.

## 9. License
[CC BY 4.0]

## 10. How to cite
Please cite this dataset: [Authors (Year). Title [Data set]. Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX]

If the related paper is published, please cite it as well (details will be added here).
