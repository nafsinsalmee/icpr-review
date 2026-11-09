# UATD Paper Review Summaries

## HSTC-MoSeg: A Hierarchical Spatially Adaptive and Temporally Consistent Network for Radar Point Cloud Moving Object Segmentation

1. **HSTC-MoSeg** introduces three modules: HCAB (local and global contextual attention), SAPConv (geometry-guided spatially adaptive convolution), and TCEM (temporal consistency enhancement) for radar point-cloud segmentation.
2. **HCAB** could be adapted to UATD to improve local and global acoustic feature extraction.
3. **SAPConv** could be modified from 3D point-based convolution to 2D spatial feature extraction to handle acoustic noise and varying target sizes.
4. **TCEM** may improve detection consistency across consecutive sonar frames, but requires sequential image data.
5. **Expected benefit:** Better feature representation and potentially improved small-target detection, mAP, and recall. The paper's reported results are from radar datasets, not UATD.
6. **Verdict:** Worth exploring by integrating adapted 2D-HCAB and 2D-SAPConv into a YOLO-based detector; UATD improvements must be experimentally validated.

## The Detector Teaches Itself: Lightweight Self-supervised Adaptation for Open-Vocabulary Object Detection

1. **The Detector Teaches Itself** proposes Decoupled Adaptivity Training (DAT), a self-supervised fine-tuning pipeline that helps a vision-language model (VLM) recognize objects at the region level for open-vocabulary object detection.
2. It uses a pretrained closed-set detector to generate region-aware pseudo-labels, including regions containing novel objects that may otherwise be unlabeled or mislabeled, and uses these data to adapt the VLM.
3. **UATD applicability:** The pipeline could be adapted to sonar imagery to help recognize underwater object categories beyond the detector's original training classes.
4. **Expected benefit:** Better region-level semantic recognition and potentially improved detection of unfamiliar object classes; improved overall mAP is possible but not guaranteed.
5. **Limitations:** The method is designed around pretrained vision-language models and conventional images. Sonar-specific visual-language alignment, reliable pseudo-labels, and domain adaptation would be essential; noisy pseudo-labels could also reinforce detection errors.
6. **Verdict:** Worth exploring as an auxiliary open-vocabulary adaptation module for a YOLO-style UATD detector, especially for unseen classes. Compare mAP, recall, and novel-class AP against the baseline and check pseudo-label quality.

## Sonar-FERT: An Accurate Detector Based on RT-DETR for Underwater Sonar Imagery

1. **Sonar-FERT** proposes an RT-DETR-based detector with a Dual Decoupled Enhancement (DDE) strategy to improve feature robustness and object localization in forward-looking sonar images.
2. It introduces **Frequency-Modulated Deformable Large Kernel Attention (FMD-LKA)** in the encoder to suppress speckle noise and extract robust features, and **Edge-Guided Attention (EGA)** in the decoder to improve boundary representation and localization.
3. **UATD applicability:** Very high. The authors explicitly evaluate the method on the **UATD-2022 dataset**, so its pipeline is directly relevant rather than requiring an RGB-to-sonar adaptation.
4. **Reported benefit:** On UATD-2022, Sonar-FERT achieves F1-scores of **87.3% and 87.6%**, with mAP values of **83.6% and 84.7%** on the reported test settings. It also reports 89.3% mAP on the Water Tank Marine Debris dataset.
5. **Limitations:** It is based on RT-DETR, so computational cost and inference speed should be checked against your current YOLO baseline. Its reported scores may also depend on the exact UATD split and evaluation protocol.
6. **Verdict:** **Highly recommended to test.** You can reproduce Sonar-FERT on UATD-2022 or selectively integrate FMD-LKA and EGA into your existing detector. It has strong potential to improve detection accuracy, but compare mAP@50, mAP@50:95, precision, recall, F1, and FPS under identical settings.
