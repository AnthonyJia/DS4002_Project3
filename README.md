# DS4002_Project3 - Classifying Facial Images as Real or Fake (AI-Generated)

## Data Devils: Anthony Jiang (leader), Laura Espuna

### Software & Platform

#### Platform Used
- Development was done primarily on **macOS (Sonoma 14.0)**.
- It should also run on **Windows 10/11** as long as **Python 3.11** and the required packages are installed.

#### Software Used
- **Programming Language:** Python 3.11  
- **Version Control:** Git & GitHub  
- **Software Environments:** Google Colab & Kaggle Notebook

### Required Packages 
The following Python packages are required to run the project: 
- `pandas` (For loading, cleaning, and manipulating tabular data (DataFrames))
- `matplotlib` (Core plotting library for creating visual graphs and charts)
- `seaborn` (Statistical data visualization library built on top of matplotlib with cleaner styles)
- `pillow` (For opening, editing, and processing images in Python)
- `numpy` (Efficient numerical computing library; supports arrays, matrices, and math operations)
- `torch` (Deep learning framework for building and training neural networks)
- `torchvision` (PyTorch’s companion for image datasets, transforms, and pretrained models)
- `scikit-learn` (Machine learning library for metrics, preprocessing, and classic ML models)
- `opencv-python` (Computer vision toolkit for advanced image processing and manipulation)

*This project was developed and tested primarily in Google Colab and Kaggle Notebooks. Both environments already include most required machine learning and scientific libraries (e.g., PyTorch, NumPy, Pandas, Matplotlib, Seaborn, Pillow, scikit-learn). So, if you are using Google Colab and/or Kaggle Notebooks, then you don't need to manually install any of these packages.*

*If you are running this project locally, you have to manually install these packages.*
- To install, run the following code:
```
pip install -r requirements.txt
```

### Map of Repository 
```
.
├── DATA
│   ├── README.md
│   ├── fake_images
│   └── real_images
├── LICENSE
├── OUTPUT
│   ├── AVG_Magnitude_Spectrum.png
│   ├── AVG_RGB.png
│   ├── Distribution_Image_Brightness.png
│   ├── FFT_AVG_Magnitude_Sample_Images.png
│   ├── Real_Fake_Distribution.png
│   ├── confusion_matrix.png
│   ├── fake_face_heatmap.png
│   ├── model_loss.png
│   ├── model_scores.png
│   ├── real_face_heatmap.png
│   └── tsne_embeddings.png
├── README.md
├── SCRIPTS
│   ├── download_data_and_eda.ipynb
│   └── model-training-testing-ipynb.ipynb
└── requirements.txt

6 directories, 17 files

```


### Instructions for Reproduction 

#### Step 0: Add Google Drive Shortcuts to datasets

For the [FFHQ dataset](https://drive.google.com/drive/folders/1tZUcXDBeOibC6jcMCtgRRz67pzrAHeHL), add shortcuts to folders (00000 - 09000) to your google drive. The `download_data_and_eda.ipynb` script expects the shortcuts to be in  Mydrive/ai_classification_dataset/ffhq/ folder on your google drive.

To add a shortcut, simply click the three vertical dots on the right side of the folder/file --> Organize --> Add shortcut.

Your folder structure should look something like this:
```
MyDrive/
└── ai_classification_dataset/
    └── ffhq/
        ├── 00000 (shortcut)
        ├── 01000 (shortcut)
        ├── ...
        └── 09000 (shortcut)
```

For the [StyleGAN dataset](https://drive.google.com/open?id=14lm8VRN1pr4g_KVe6_LvyDX1PObst6d4), go into the `psi-0.7` folder, add shortcuts to the **zipped** folders (000000 - 009000) to your google drive. The `download_data_and_eda.ipynb` script expects the shortcuts to be in  Mydrive/ai_classification_dataset/stylegan/ folder on your google drive. 

Your folder structure should look something like this:
```
MyDrive/
└── ai_classification_dataset/
    └── stylegan/
        ├── 000000.zip (shortcut)
        ├── 001000.zip (shortcut)
        ├── ...
        └── 009000.zip (shortcut)
```

#### Step 1: Download the data into the Google Colab environment and perform exploratory data analysis

Open the `download_data_and_eda.ipynb` script in Google Colab environment and run it. 

This script does the following:
- Downloads the image data from NVIDIA's NVlabs research team's google drive via the shortcuts you made on your google drive
- Counts the number of real images (ffhq) and fake images (stylegan)
- Displays a sample of real images (ffhq) and fake images (stylegan)
- Performs EDA (color distribution, brightness, texture/level of detail)
- Zips the datasets on the virtual Google Colab environment and downloads them on your local computer (This is required for Step 2)

#### Step 2: Model Training, Testing, and Evaluation

Open the `model-training-testing.ipynb` script in Kaggle Notebook environment. 

*Sidenote: You will need to create a Kaggle account to use the Kaggle Notebook environment (it's free)*

The reason why we use the Kaggle Notebook environment to run the second script is because Kaggle provides free GPUs, which speeds up the process of training deep neural networks such as convolutional neural networks. 

Before you can run the script, you have to upload the datasets you zipped in step 1 to the Kaggle Notebook environment. Simply open the right side menu of the notebook. Under the input section, click Upload --> New Dataset --> upload real_images.zip, fake_images.zip. For the dataset title, name it `human-faces`. This will take a while, since we are uploading 20k images to the environment. 

After the datasets are done uploading, you can run the script. 

This script does the following: 
- Counts the number of real images (ffhq) and fake images (stylegan)
- Preprocesses the image data for the chosen CNN model (Resnet18)
- Trains the model
- Tests the model
- Display evaluation metrics (Accuracy, Precision, Recall, F1-score) and confusion matrix
- Creates t-SNE embedding chart to visualize whether there are clear clusters forming between the real images and fake images
- Creates heatmaps on certain images to show which areas the model analyzed to classify whether an image is real or fake
