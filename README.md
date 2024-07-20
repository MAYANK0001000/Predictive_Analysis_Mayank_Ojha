Here's a more organized and detailed breakdown of the instructions provided for your project, formatted as a step-by-step guide. This should help in setting up the environment, creating YOLO datasets, training, validating the model, and testing with existing data.

---

# Predictive Analysis End Project Guide

This guide helps convert Labelstudio export and video data into YOLO training data, train a YOLO model, and validate it using uploaded videos.

---

## System Preparations

### Windows Setup (similar for Linux, without WSL addition)

1. *Install Visual Studio Code*
   - Download from [Visual Studio Code](https://code.visualstudio.com/Download)

2. *Install WSL and Upgrade to Version 2*
   - Follow [WSL Installation Guide](https://learn.microsoft.com/de-de/windows/wsl/install)

3. *Install FFmpeg on Windows*
   - Instructions available [here](https://www.geeksforgeeks.org/how-to-install-ffmpeg-on-windows/)

4. *Install WSL Extension in Visual Studio Code*
   - Follow the [VS Code WSL Extension Guide](https://code.visualstudio.com/docs/remote/wsl)

5. *Open Ubuntu Console*
   - Open via PowerShell dropdown or type ubuntu in console

6. *Clone Project from GitHub and Navigate into Path*
   sh
   git clone https://github.com/kroggeryy/predictiveAnalysisEndproject.git
   cd predictiveAnalysisEndproject
   

7. *Install FFmpeg on Linux*
   sh
   sudo apt install ffmpeg
   

8. *Create and Activate Virtual Environment*
   - Follow the [Virtual Environments Guide](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)
   sh
   python3 -m venv .venv
   source .venv/bin/activate
   

9. *Upgrade pip*
   sh
   python3 -m pip install --upgrade pip
   python3 -m pip --version
   

10. *Install Requirements*
    sh
    pip install -r requirements.txt
    

11. *Open Project in VS Code*
    sh
    code .
    

---

## Creating YOLO Data Yourself

1. *Delete Current YOLO Model if Exists*
   - Remove files like yolov8n.pt

2. *Create New Folder for Sample Data*
   - Name it something like sampledata2

3. *Run Script to Create YOLO Dataset*
   sh
   python 01-createYoloDataset.py -l sourceMaterial/LabelStudioExport.json -v sourceMaterial/LabelStudioVideo.mp4 -o sampledata -s 20 -r 30
   

4. *Edit Dataset Path in Ultralytics Configuration*
   - Open settings.yaml in /home/.config/Ultralytics
   - Reference your newly created folder based on 00-setting.yaml

5. *Train YOLO Model*
   sh
   python 02-trainYoloModel.py
   

6. *Validate YOLO Model*
   sh
   python 03-validateYoloModel.py ./validationVideos/"videotitle".mp4 -o ./validationResultVideos/outputName.avi
   

---

## Training YOLO Model with Existing Data

1. *Delete Current YOLO Model if Exists*
   - Remove files like yolov8m.pt

2. *Edit Dataset Path in Ultralytics Configuration*
   - Open /home/.config/Ultralytics
   - Reference the folder dataset based on 00-setting.yaml

3. *Train YOLO Model*
   sh
   python 02-trainYoloModel.py
   

4. **Upload Validation Video to Folder validationVideos**

5. *Configure Validation Script*
   - Go to path sampledata/runs/detect, under the last train folder
   - Select best.pt model
   - Copy the relative path and paste it into the script
   python
   model = YOLO("relative path")
   

6. *Run Validation Script*
   sh
   python 03-validateYoloModel.py ./validationVideos/"videotitle".mp4 -o ./validationResultVideos/outputName.avi
   

7. *Optional: Preview Validation*
   sh
   python 03-validateYoloModel.py ./validationVideos/"videotitle".mp4 -p --preview -o ./validationResultVideos/outputName.avi
   

---

## Testing with Pre-Trained YOLO Model

1. **Upload Validation Video to Folder validationVideos**

2. *Run Validation Script*
   sh
   python 03-validateYoloModel.py ./validationVideos/"videotitle".mp4 -o ./validationResultVideos/outputName.avi
   

3. *Optional: Preview Validation*
   sh
   python 03-validateYoloModel.py ./validationVideos/"videotitle".mp4 -p --preview -o ./validationResultVideos/outputName.avi
   

---

By following this detailed guide, you can set up your environment, create and train YOLO datasets, and validate the model using your videos. Make sure to adjust file paths and names as needed for your specific setup.