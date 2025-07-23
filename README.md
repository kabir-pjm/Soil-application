

# SoilAI - Smart Soil Analysis & Crop Recommendation System


SoilAI is an intelligent web application designed to assist farmers and agricultural enthusiasts in making informed decisions about soil health and crop cultivation. By leveraging image recognition for soil type identification and machine learning models for crop and fertilizer recommendations, SoilAI provides a comprehensive solution for optimized agricultural practices.

## ✨ Features

  * **Soil Image Analysis:** Upload an image of your soil sample to automatically detect its type (e.g., Black, Cinder, Laterite, Peat, Yellow).
  * **Detailed Soil Characteristics:** Get insights into the composition, pH range, drainage, and fertility of the detected soil type.
  * **Soil Parameter Input:** Manually enter key soil parameters such as temperature, humidity, moisture, nitrogen (N), phosphorous (P), potassium (K), and pH value.
  * **Crop Recommendation:** Receive personalized crop recommendations based on your soil's characteristics and entered parameters.
  * **Fertilizer Recommendation:** Get suggestions for the most suitable fertilizers, including their NPK ratios and application details.
  * **Soil Problem Diagnosis:** Identify potential soil deficiencies, excesses, or structural issues with suggested solutions.
  * **Seasonal Management Calendar:** Access a tailored calendar with soil management tasks specific to your soil type and recommended crop.
  * **Watering Advice:** Receive detailed guidance on watering schedules, amounts, and methods, adjusted for soil type and environmental conditions.
  * **Comprehensive Report Generation:** Generate a downloadable report summarizing all analysis, recommendations, and management plans.
  * **Interactive Visualizations:** Understand your soil's nutrient levels and NPK balance through intuitive charts (powered by Plotly).

## 🚀 Technology Stack

  * **Backend:** Flask (Python)
  * **Frontend:** HTML, CSS (Bootstrap 5), JavaScript
  * **Machine Learning:**
      * **Image Classification:** TensorFlow/Keras (EfficientNetB0 for soil type detection)
      * **Tabular Data Classification (Crop/Fertilizer):** XGBoost
      * **Data Preprocessing:** scikit-learn (LabelEncoder, StandardScaler), Imblearn (SMOTE)
  * **Data Handling:** Pandas
  * **Visualizations:** Matplotlib, Seaborn, Plotly
  * **Deployment:** Designed for local deployment or containerization (e.g., Docker)

## 🛠️ Installation and Setup

### Prerequisites

  * Python 3.8+
  * `pip` (Python package installer)
  * `git`

### Steps

1.  **Clone the Repository:**

    ```bash
    git clone (https://github.com/kabir-pjm/Soil-application.git) 
    cd SoilAI
    ```

2.  **Create a Virtual Environment (Recommended):**

    ```bash
    python -m venv venv
    ```

3.  **Activate the Virtual Environment:**

      * **On Windows:**
        ```bash
        .\venv\Scripts\activate
        ```
      * **On macOS/Linux:**
        ```bash
        source venv/bin/activate
        ```

4.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

    *(If `requirements.txt` is not yet created, you can generate it from your Colab environment or manually list the dependencies. A typical `requirements.txt` is provided below for reference.)*

    ```
    Flask
    tensorflow==2.x.x # Use the exact version from your Colab notebook
    Pillow
    plotly
    matplotlib
    seaborn
    scikit-learn
    xgboost
    pandas
    imbalanced-learn
    # werkzeug (usually installed with Flask, but can add if issues)
    # google-colab (only needed if running notebooks in Colab, not for local app.py)
    # tree (for directory listing, not a core app dependency)
    ```

5.  **Prepare Data:**

      * **Place your `soil_data.csv`:** Ensure your main dataset CSV file is placed in the `soil_data/` directory. If the directory doesn't exist, create it:
        ```bash
        mkdir -p soil_data
        cp /path/to/your/soil_data.csv soil_data/
        ```
      * **Place your soil images ZIP:** Extract your soil images ZIP file directly into the main project directory. The extraction process will then move them into the correct `soil_images/` structure. The ZIP file should ideally contain a folder named "Soil types" with subfolders for each soil category (e.g., `Soil types/Black Soil/`).
        ```bash
        unzip /path/to/your/soil_images.zip -d . # Extracts to current directory
        # The data_processing script expects the 'Soil types' folder inside 'temp_soil_images'
        # You might need to adjust this step if your zip extracts differently.
        # Alternatively, manually organize your 'soil_images/' directory as follows:
        # soil_images/
        # ├── Black Soil/
        # │   ├── black_soil_001.jpg
        # │   └── ...
        # ├── Cinder Soil/
        # │   ├── cinder_soil_001.jpg
        # │   └── ...
        # └── etc.
        ```
        *(**Note for Local Setup:** The `data_processing.py` script provided in the Colab notebook uses `google.colab.files.upload()` and `!rm -rf` commands which are specific to Google Colab. For local execution, you will need to adapt the data preparation part of the script. The goal is to have `soil_data/soil_data.csv` and the `soil_images/` directory structure as shown above.)*

6.  **Run the Data Processing Script:**
    Execute the Python script containing the data processing logic. This will clean the CSV, perform feature engineering, and set up image data generators. It also handles moving images to the correct structure if extracted into `temp_soil_images`.

    ```bash
    python data_processing.py
    ```

7.  **Build and Train Models:**
    Run the Python script that contains the model building and training logic. This will train the image classification model (EfficientNet), and the crop and fertilizer recommendation models (XGBoost), saving necessary artifacts like `best_image_model.h5`.

    ```bash
    python model_building.py
    ```

8.  **Start the Flask Application:**
    Once the models are trained and saved, start the Flask web application. Ensure all necessary functions (diagnostic, response preparation) and models are correctly imported or defined within your `app.py`.

    ```bash
    python app.py
    ```

    The application should now be running. You will typically see output like:

    ```
     * Serving Flask app 'app'
     * Debug mode: off
     WARNING: This is a development server. Do not use it in a production deployment.
     Use a production WSGI server instead.
     * Running on http://127.0.0.1:5000
    ```

    Open your web browser and navigate to the provided URL (e.g., `http://127.0.0.1:5000/`).

## 👨‍🌾 Usage

1.  **Home Page:** Access the main interface of SoilAI at `http://127.0.0.1:5000/`.
2.  **Upload Soil Image (Step 1):** Click "Choose File" and upload a clear image of your soil sample. Then click "Analyze Soil". The system will detect the soil type and display its characteristics.
3.  **Enter Soil Parameters (Step 2):** Adjust the pre-filled or manually enter your measured soil parameters (Temperature, Humidity, Moisture, pH, Nitrogen, Phosphorous, Potassium).
4.  **Get Recommendations:** Click "Get Recommendations" to receive personalized crop and fertilizer recommendations, along with detailed nutrient information, soil problem diagnoses, management calendars, and watering advice.
5.  **Explore Results:** Navigate through the tabs in the "Results Section" (Summary, Nutrients, Soil Issues, Management, Water Advice) to view different aspects of the analysis.
6.  **Generate Report:** Click "Generate Report" to create a comprehensive summary of the analysis and recommendations, which can be downloaded.

## 📁 Project Structure (Expected after setup)

```
SoilAI/
├── templates/
│   └── index.html
│   └── report_template.html (if you have one for report generation)
├── static/
│   ├── training_history.png         
│   ├── crop_confusion_matrix.png    
│   ├── fertilizer_confusion_matrix.png 
│   ├── soil_chart_<session_id>.png   
│   ├── soil_report_<session_id>.json 
│   └── banner.png                    
├── uploads/
│   └── (user-uploaded soil images for analysis are stored here temporarily)
├── soil_images/
│   ├── Black Soil/
│   │   └── ... (image files)
│   ├── Cinder Soil/
│   │   └── ... (image files)
│   └── ... (other soil type directories with images)
├── soil_data/
│   └── soil_data.csv                 # Your primary dataset CSV
├── best_image_model.h5               # Trained Keras model for image classification
├── app.py                            # Flask application main file
├── data_processing.py                # Script for data loading, cleaning, preprocessing
├── model_building.py                 # Script for building and training ML models
├── requirements.txt                  # List of Python dependencies
├── README.md                         # This file
└── LICENSE.md                        # Project license details
```

## 🤝 Contributing

Contributions are welcome\! If you'd like to contribute, please follow these steps:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/your-feature-name`).
3.  Make your changes.
4.  Commit your changes (`git commit -m 'Add new feature'`).
5.  Push to the branch (`git push origin feature/your-feature-name`).
6.  Open a Pull Request.
