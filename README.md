# Adversarial Protection in Face Forgery Detection
  This project reproduces the backdoor attacks on models trained to detect face forgeries, examining how these attacks impact the model's ability to distinguish between real and fake faces.
  The project also explores defense mechanism to identify and neutralize these attacks without comprimising the model's performance<br>

  [link to the findings and comprehensive report](https://drive.google.com/file/d/19dICnPXcaYSrgrU3HtvcrESikHkwM5ko/view?usp=drive_link)

# setup the project
The code was run on Ubuntu with the following setup:

1. Install Python 3.10.x

2. From the terminal, run the following:

   ```bash
   pip3 install -r requirements.txt
and also code was run on kaggle notebooks for accessing GPUs, so make sure to change the paths for using any file in the code depending on whether you are running the code on your local machine or any cloud services like google colab/kaggle.

# Dataset preparation
we use three datasets from kaggle:
1. **Fakeforensics++** and **celebDF(V2)**: These have both real and fake faces made with different deepfake techniques.
2. **Real-v/s-Fake**: This has real and fake faces made with styleGAN
here are the links:<br>
   i)[CelebDF(v2)](https://drive.google.com/file/d/1bmBvCR3R4h_aIpisXOQpy-MqJKN_M_Uk/view?usp=drive_link)<br>
  ii)[Faceforensics++](https://drive.google.com/file/d/1KDMFUdNPZ1fVKcZMhh0OJ0939rHnlv00/view?usp=drive_link)<br>
 iii)[Real-v/s-Fake](https://drive.google.com/file/d/1eqNqWSSVk3eHjvZqXYsVk_fDTgwKQfkr/view?usp=drive_link)<br>
 The datasets links uploaded here are preprocessed.In general, to extract facial regions from video frames in the dataset, a pre-trained face landmark detection model is utilized. The implementation of this process is available in the file `src/preprocess/crop_dlib.py`.


Download the pre-trained face landmark detection model [here](https://github.com/VamshiNarmety/Adversarial-Protection-in-Face-Forgery-Detection/blob/main/src/preprocess/shape_predictor_81_face_landmarks.dat)<br>

# Test model on clean Datasets
After setting up the dataset, you can train and test the model on clean,unmodified datasets to ensure it works well on clean data.<br>
**Train the model:** To train the model on clean datasets, run the `train_test_model(cleandata).py` file.
- The purpose of testing on clean data is explicitly mentioned to ensure the model works well before proceeding to the attacks.

# Trigger generator(Backdoor attack)
Run the `src/utils/trigger_generator.py` file to train the trigger generator for backdoor attacks and save the model.

# Train model on Backdoor attacked data
- Run the `backdoor_attacked_model.py` file to poison the datasets and prepare them for training the model. This script modifies the datasets by injecting backdoor triggers.
- save the models.

# Backdoor detection and purification
- Run the `ipynb` files for the detection and purification of the attacks.
- The code for the functions used in these `ipynb` files is present in `src/defender/bd_detection.py` and `src/defender/backdoor_purification.py`.
- Make slight changes in the code of the files in `src/defender/` depending on the model architecture and the layers you are considering for the defense mechanism.

# Note
- Ensure you modify paths appropriately when switching between local environments and cloud-based platforms (Google Colab, Kaggle).
- Make sure you adjust the code in the defender files (bd_detection.py, backdoor_purification.py) as needed, based on your model's architecture and layers considered for defense.
- If the dataset is too large, load a portion using code present in `src/utils/Dataset_loader.py`. This code is implemented based on the dataset's file structure used in this project and Generally, should be updated if the structure changes i.e, if other datasets were used.
