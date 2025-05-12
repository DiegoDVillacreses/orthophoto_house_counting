# orthophoto_house_counting

This repository presents an automated pipeline for detecting and counting residential structures in high-resolution orthophotos using Meta’s [Segment Anything Model (SAM)](https://github.com/facebookresearch/segment-anything) in conjunction with heuristic filtering.

## Methodology

### Data Preparation
Input orthophoto is divided into overlapping tiles to avoid VRAM collapse. Then, each tile is standardized.

### Segmentation with SAM

SAM (a general-purpose, class-agnostic segmentation model) is used to generate masks for objects in each tile for further filtering.

## Heuristic Filtering
We use the following filters:
* Size/shape: keep masks with area, compactness, and aspect‐ratio within bounds
* Border check: drop patches with very low mean intensity
* Vegetation filter: reject if mean ExG or HSV‐green ratio is too high
* Shape filter: require solidity and rectangularity above thresholds
* NMS: remove overlapping boxes (IoU < 0.3)

## Installation

Follow [Segment Anything Model (SAM)](https://github.com/facebookresearch/segment-anything) installation instructions, verify that you have a valid `torch` installation compatible with your hardware.

## Results
<img src="https://github.com/user-attachments/assets/96ab0b43-a585-4e62-9841-ad2eba0224a6" width="400"/>
<img src="https://github.com/user-attachments/assets/9bfaefad-dc71-4e0f-96d7-22a6608802fd" width="400"/>

## Further research
* Compare results with human labelled information.
* Add LiDAR information expecting higher accuracy as suggested by: https://github.com/Wang-wei-lin/SAM_based_Building_Footprint_Extraction_for_Residential/tree/master
