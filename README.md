# Framework for Enhancing Geospatial Label Accuracy of RTS Using AI
## 1. Introduction
This project introduces a fully automated pipeline to **update outdated labels of Retrogressive Thaw Slumps (RTS)** using cutting-edge **zero-shot AI segmentation models**. Leveraging prompt-based models such as **Segment Anything (SAM and SAM2)**, the system produces **refined and up-to-date boundary masks** that align with the latest satellite imagery.

The pipeline operates through a **multi-stage process**:
1. **Initial RTS boundary proposals** are paired with current satellite imagery.
2. **Model-ready prompts** (point, box, and mask-based) are generated.
3. The **SAM models** process these prompts to produce multiple segmentation outputs.
4. Outputs are **ranked by Intersection over Union (IoU)** against known ground truth.
5. Results undergo **expert validation** and can be approved using a **review dashboard**.

To support transparency, validation, and scaling, the framework includes:
- A **Utility Dashboard** for prompt/mask inspection and debugging,
- A **Review Dashboard** for expert approval of high-quality masks (with manifest updates),
- And an **Analytics Dashboard** showing IoU distributions and performance breakdowns by level, complexity, and prompt type.

By significantly **reducing manual effort** and maintaining **high segmentation quality**, this pipeline offers a powerful, scalable, and modular approach to monitoring **dynamic permafrost landscapes**—with potential for broader application across diverse environmental phenomena.

## Key Features

- **High-Quality Automated Delineation**  
  Produces segmentation masks that closely match expert-drawn RTS boundaries while drastically reducing manual labeling time.
- **Zero-Shot Generalization**  
  Uses prompt-based AI models (SAM and SAM2) that do not require task-specific training, enabling generalization across diverse and unseen RTS instances.
- **Multi-Stage Prompting Pipeline**  
  Combines existing labels with up-to-date satellite imagery to generate model-ready prompts that enhance segmentation accuracy.
- **Expert Validation Workflow**  
  Integrates ground-truth comparisons and interactive visualization tools to facilitate expert review, ensuring accuracy and reliability of the generated polygons.
- **Utility Dashboard for Debugging**  
  Enables on-demand inspection of inputs, prompts, and all SAM-generated masks ranked by IoU for in-depth analysis of segmentation behavior.
- **Review Dashboard for Human-in-the-Loop Selection**  
  Empowers experts to approve the most accurate segmentation output per image, automatically updating the manifest and organizing approved data.
- **Analytics Dashboard for Performance Insights**  
  Provides visual summaries—including IoU distributions, max IoU per level/complexity, and prompt-type breakdowns—supporting quantitative evaluation and model tuning.
- **Scalability and Modularity**  
  Built for reproducibility and scalability, supporting large-scale and longitudinal monitoring of remote and complex permafrost terrains.
- **Broad Applicability**  
  While designed for RTS, the framework is adaptable to other dynamic environmental features, offering a generalized solution for improving geospatial labels in evolving landscapes.
---

## 2. Workflow Overview

![Workflow Pipeline](docs/Workflow%20Pipeline.png)

---

## 3. How to Use (via Google Colab)
### Steps

This pipeline is designed to run entirely in **Google Colab**, so no local installation is required. The only requirement is access to a Google Drive account to store models, data, and results.
#### 1. Authenticate Your Google Account
  - You will be prompted to authenticate your Google account. This is required to:
    - Mount your Google Drive (for reading/writing data, checkpoints, and outputs)
    - Access any shared folders used by the pipeline
- **Instructions:**
  - Run the first cell in any notebook to trigger the authentication.
  - Follow the on-screen instructions to log in and **grant access** to your Google Drive.  
  - This step will repeat in each notebook. You must authenticate once per session.

#### 2. Setup SAM Models & Checkpoints
- Before running the segmentation notebooks, you need to download the **SAM model checkpoints** and set them up in your   Google Drive.
- Run setup notebook in Google Colab:
   [SAM_setup.ipynb](https://github.com/whrc/img-label-correction-SAM/blob/main/src/SAM_setup.ipynb)
- This will automatically install the required SAM and SAM2 code and checkpoints into the google drive under `SAM` and `SAM2` directories.

#### 3. Organize Input Data based on Complexity & Quality Labels
  - Ensure the raw satellite imagery, RTS starting polygon data and ground truth polygon data are available in the data/raw/ folder within your Google Drive
  - Each satellite image and its corresponding RTS polygon are categorized based on two criteria: **Fixability Level** and **Quality Issue Type**. These categories help guide both automatic processing and expert review.
  - These annotations are included in the manifest and are critical for evaluating SAM model performance across different scenarios.
  - Fixability Level (1–3):   
    Indicates how difficult it is to correct the RTS boundary:
    
    | Level | Description |
    |-------|-------------|
    | **Level 1 (Easy)**   | The RTS polygon is mostly accurate and only requires minor adjustments (e.g., slight shift or a few added vertices). |
    | **Level 2 (Moderate)** | The RTS is somewhat misaligned or simplified; requires moderate edits like shifting and adding several vertices. |
    | **Level 3 (Hard)**   | The RTS polygon is significantly incorrect. It's easier to redraw the entire polygon than to fix the existing one. |

  - Quality Issue Type (A–C):   
    Describes the type of issue present in the original RTS polygon:
    
    | Code | Issue Type           | Description |
    |------|----------------------|-------------|
    | **A** | Spatial Mismatch     | The RTS polygon is correctly shaped but **offset** from the actual feature in the imagery (e.g., shifted location). |
    | **B** | Simplistic Mismatch | The polygon is correctly located but **overly simplified** (e.g., lacks sufficient detail or vertices). |
    | **C** | Time Mismatch        | The polygon was drawn using **older imagery**, so it’s smaller or outdated compared to the current RTS footprint. |

---
## 4. Contributing
Contributions to this project are welcome. Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix (git checkout -b feature/your-feature-name).
3. Make your changes and commit them with clear, descriptive messages.
4. Push your changes to your fork (git push origin feature/your-feature-name).
5. Create a new Pull Request against the main repository.
---
## 5. License
This project is licensed under the MIT License - see the LICENSE file for details.
