# **GBC preoperative T-Staging prediction v1.0- User Manual**

Thank you for using the GBC preoperative T-Staging prediction v1.0! 
This application is based on a multimodal fusion model (FWM) that integrates clinical features, radiomics, 
and deep learning characteristics to provide preoperative staging predictions.
Below is a detailed user manual to help you maximize the potential of this tool.

---

## **Introduction**

This prediction application is designed for preoperative T-staging of gallbladder cancer (GBC),
combining radiomics and deep learning features extracted from contrast-enhanced CT (CECT) images 
with patients' clinical baseline data. The outputs include stage classification (T2 or below / T3 or above) 
and corresponding probabilities, providing valuable guidance for surgical planning.

> **Note**:
> Feature extraction involves heavy computation, especially for deep learning models. The time required to process data depends on the number of patients uploaded. If your system does not have CUDA support (GPU acceleration), the process will take longer. Even if the program appears unresponsive, it is still running in the background. Please be patient during this phase.

---

## **User Guide: Program Requirements and Recommendations**

To ensure the program operates optimally and meets its intended purpose, please adhere to the following recommended and minimum system configurations:

### **Recommended Configuration for Best Performance**
- **Operating System**: Windows 10 / 11, 64-bit
- **Python Environment**: Python 3.8+
- **Deep Learning Framework**: PyTorch 2.4.0+cu124, TorchVision 0.19.0+cu124
- **Hardware**:
  - **Recommended**: CUDA-supported GPU (e.g., NVIDIA RTX series) for GPU acceleration
  - **Minimum**: CPU-based execution (slower performance)

### **Minimum System Requirements**
- **CPU**: Intel i5 or higher
- **Memory**: 8 GB RAM or more
- **Storage**: Approximately 10 GB (program + weight files)
- **Network**: A stable internet connection is required for online weight loading (if applicable)

> **Fallback for Offline Systems**:
> If the system does not have internet access or does not meet the above conditions, the program will automatically use the pre-provided local weight files stored in the "_internal" folder. However, results may have slight deviations compared to those obtained using the latest official weights.

---

## **Usage Instructions**

### 1. application Dependencies
- All sub-files within the application folder are essential for its operation. Please avoid deleting or moving any files.
- Pay special attention to the files in the "data" folder. Missing any of these files might lead to application failure.

### 2. Data Preparation
Before uploading patient image data for prediction:
- Ensure that arterial-phase (AP) and portal venous-phase (PVP) CECT images for GBC patients have undergone ROI segmentation.
- Both images and their corresponding masks should be saved in NIFTI format, with matching sequence numbers.
- **File naming format example**:
  - Arterial phase image: `AP-image8`
  - Arterial phase mask: `AP-mask8`
  - Portal venous phase image: `PVP-image8`
  - Portal venous phase mask: `PVP-mask8`

> **Note**:  
> ROI segmentation can be performed using open-source tools like [3D Slicer](https://www.slicer.org/) or [ITK-SNAP](http://www.itksnap.org/).  
> Incomplete image data or incorrect formats will result in prediction failure.

### 3. Batch Uploading
- **Batch Upload**: It is recommended to upload data for multiple patients at once to enhance efficiency.
- **Random Seed**: To ensure consistent results, use a fixed random seed (recommended value: `5420`).

### 4. Manual Input of patient's Baseline characteristics
For each patient, clinical baseline data must be manually entered in sequence. Follow these guidelines for input:
- **Sex**: 0-Female, 1-Male  
- **Age**: in years  
- **Smoking History**: 0-No, 1-Yes  
- **Gallbladder Polyps**: 0-No, 1-Yes  
- **Gallbladder Stones**: 0-No, 1-Yes  
- **Gallbladder Wall Thickening (≥5mm)**: 0-No, 1-Yes  
- **Size**: in millimeters (mm)  
- **Lymphatic Node Metastasis**: 0-No, 1-Yes  
- **Distant Metastasis**: 0-No, 1-Yes  
- **Tumor Margin**: 0-Blur, 1-Clean  
- **Serological Data**: ALP(U/L), TB(umol/L), ALB(g/L), ALT(U/L), AST(U/L), AFP(ng/ml), CA19-9(U/ml), CA125(U/ml), CEA(ng/ml)

> **Note**:  
> If there are any indicators with decimal values, only one decimal place needs to be entered.

### 5. Results Storage
- After prediction, results will be saved automatically in an Excel file in the application's subdirectory:
  - If you click the “**continues**” button: The results will be stored under `\Prediction result x\Postpredict-Final predicted probabilityinal_weighted_prediction.xlsx`, and the next round of predictions will begin automatically.
  - If you click the “**close**” button: The results will be stored under `\The last Prediction result\Postpredict-Final predicted probabilityinal_weighted_prediction.xlsx`, and the application will terminate.

> **Note**:  
> In Prediction result x, the x represents a number that increments with each prediction round.

---

## **Operational Steps**

1. **Upload Image Data**: Batch upload preoperative arterial-phase (AP) and portal venous-phase (PVP) CECT images and their corresponding masks for GBC patients.
2. **Input Random Seed**: Use the recommended value (e.g., 5420).
3. **Input Clinical Features**: Manually input baseline data for each patient as prompted.
4. **Run Prediction**: The application will output predictions, including classifications (T2 or below / T3 or above) and probabilities.
5. **Save Results**: Choose “continues” or “close” to save results and proceed accordingly.

---

## **Important Notes**

- This application is suitable for GBC patients with complete preoperative image and clinical data.
- If issues arise during operation, verify the completeness and accuracy of uploaded files and input data.
- **Results are for reference only**: The predictions are intended as an auxiliary tool. Final clinical decisions should consider all dimensions of patient information.

---

## **Acknowledgments**

Thank you for supporting this prediction application! As the application is still under testing, we appreciate your feedback for further improvement. For inquiries, please contact the development team or refer to the technical documentation.
