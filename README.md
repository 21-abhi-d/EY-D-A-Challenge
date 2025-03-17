# **Urban Heat Island (UHI) Index Prediction Project**

## **Project Overview**
This project predicts the **Urban Heat Island (UHI) Index** using remote sensing data from Sentinel and Landsat satellites. The goal is to train a **Random Forest Regressor** model on extracted satellite features and use it to generate predictions for test locations.

## **Data Sources**
- **Sentinel-2 Data**: Extracted from GeoTIFF files containing spectral band information.
- **Landsat Data**: Provides Land Surface Temperature (LST) values.
- **Ground Truth Data**: CSV file containing UHI index values for training locations.
- **Submission Template**: CSV file with latitude & longitude for test locations.

## **Workflow**
### **1. Data Processing**
- **Extract spectral bands** (`B01`, `B04`, `B06`, `B08`) from **Sentinel-2** data.
- **Compute Vegetation Indices**: NDVI, NDWI, NDBI, EVI, SAVI, BI.
- **Extract LST (Land Surface Temperature)** from **Landsat** data.
- **Merge extracted features** with ground truth UHI data for training.

### **2. Model Training**
- **Preprocess features** (remove missing values, normalize features).
- **Train a Random Forest Regressor** using extracted features.
- **Evaluate model performance** using R² score on test data.
- **Save trained model and scaler** for future predictions.

### **3. Prediction & Submission**
- **Load test location coordinates** from the submission template.
- **Extract corresponding Sentinel-2 and Landsat features**.
- **Apply feature scaling using the saved scaler**.
- **Predict UHI Index values** using the trained model.
- **Generate `submission.csv` file** for final evaluation.

## **File Structure**
```
├── datasets/
│   ├── S2_sample.tiff         # Sentinel-2 GeoTIFF file
│   ├── Landsat_LST.tiff       # Landsat LST GeoTIFF file
│   ├── Training_data.csv      # Training data with UHI index
│   ├── Submission_template.csv # Test locations for submission
│
├── scripts/
│   ├── preprocess.py          # Extract & process satellite features
│   ├── train_model.py         # Train and save Random Forest model
│   ├── predict.py             # Generate UHI predictions for test data
│
├── models/
│   ├── random_forest_model.pkl # Saved trained model
│   ├── scaler.pkl             # Saved feature scaler
│
├── submission.csv             # Final predicted UHI Index for submission
├── README.md                  # Project documentation
```

## **Installation & Setup**
### **1. Install Dependencies**
```bash
pip install numpy pandas rioxarray scikit-learn tqdm joblib pyproj
```

### **2. Run the Scripts**
#### **Step 1: Preprocess Data**
```bash
python scripts/preprocess.py
```
#### **Step 2: Train the Model**
```bash
python scripts/train_model.py
```
#### **Step 3: Generate Predictions**
```bash
python scripts/predict.py
```

## **Troubleshooting & Notes**
- Ensure the TIFF files are correctly placed inside `datasets/`.
- If a feature mismatch occurs during prediction, verify that the **same features** were used in training and testing.
- The **scaler.pkl** file must be used when transforming test data before prediction.

## **Authors & Acknowledgments**
- **Developed by:** Abhishek Deshpande, Purva Patil, Joshua Kim
- **Special Thanks:** EY Global
- **Data Sources:** ESA Sentinel-2, NASA Landsat

## **License**
This project is for educational and research purposes only.