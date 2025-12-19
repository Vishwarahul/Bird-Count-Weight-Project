# Bird Counting and Weight Estimation from CCTV Video
## Overview

This project is a prototype AI/ML system that analyzes a fixed-camera poultry CCTV video to:

Count birds over time using detection and tracking

Estimate bird weight using a visual weight proxy

Generate an annotated output video

Expose the full pipeline through a FastAPI service

The solution uses pretrained models and does not require labeled training data.
## Problem Understanding

Given a poultry CCTV video:

Detect birds in each frame

Assign stable tracking IDs to avoid double counting

Count birds over time

Estimate bird weight or a relative weight index

Provide results via an API
## Approach Summary

Bird Detection

Used YOLOv8 pretrained model

Detects birds and outputs bounding boxes with confidence

Bird Tracking

Used ByteTrack tracker

Assigns stable IDs across frames

Handles occlusion and temporary disappearance

Bird Counting

Counted unique active tracking IDs per frame

Avoids double counting

Weight Estimation

Real weight ground truth is unavailable

Used bounding box area as a relative weight index

Averaged area over time for stability

Confidence based on size variation

Frame Sampling

Video processed at 5 FPS

Reduces computation

Suitable because bird movement is slow

Weight Estimation Details

Current Output

Unit: index (relative weight)

Larger index indicates heavier bird

How to Convert to Grams
To convert weight index into real grams, one of the following is required:

Camera calibration with real-world scale

Reference object of known size in the frame

Small labeled dataset mapping pixel area to bird weight

After calibration:
Weight (grams) = a × pixel_area + b
## Data Source

Publicly available poultry CCTV / chicken farm video

Used only for demonstration purposes

Fixed camera assumption applied
## Assumptions

Camera is fixed

Birds are roughly on the same ground plane

No true weight labels available

Weight proxy used instead of real grams
## Conclusion

This prototype demonstrates a complete end-to-end AI pipeline for poultry monitoring using:

Detection

Tracking

Counting

Weight proxy estimation

API deployment

The system is modular, explainable, and extendable for real-world calibration and deployment.
