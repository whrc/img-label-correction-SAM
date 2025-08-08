# Framework for Enhancing Geospatial Label Accuracy of RTS Using AI
## 1. Introduction

This project automatically improve outdated labels of Retrogressive Thaw Slumps (RTS) to match the latest satellite imagery by leverages zero-shot AI segmentation models. It employs a multi-stage process where initial RTS boundary proposals are used alongside current imagery to generate model-ready prompts for AI segmentation. It then utilizes a prompt-based segmentation model, the Segment Anything Model(SAM and SAM2), to derive refined, up-to-date RTS boundary masks. To ensure high quality, these new delineations are validated against expert-annotated ground truth. Furthermore, a visualization interface is provided for comprehensive expert review and quality control, offering both analytical summaries and interactive visual inspection of the generated outputs, helping to confirm the most accurate new polygons.

## Key Features
- This framework significantly improves upon existing RTS digitization by producing comparable delineations to those created manually while significantly reducing the label generation time.
- Its modular and reproducible design also supports scalable monitoring of diverse and remote permafrost landscapes.
- The inherent zero-shot capability of our method further extends its applicability beyond RTS, offering a versatile solution for enhancing object label quality across various dynamic environmental phenomena captured in satellite imagery.
---

## 2. Workflow Overview

![Workflow Pipeline](docs/Workflow%20Pipeline.png)

---


