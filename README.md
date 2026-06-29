# License Plate Detection + OCR Pipeline

A Python-based automatic license plate detection and recognition system built with **YOLOv8** and **EasyOCR**.

This project processes all images inside the `Testing/` folder, detects license plates, extracts the plate text, and saves annotated outputs. It includes advanced preprocessing steps to improve OCR performance on difficult images such as low-light, blurry, skewed, noisy, or glare-affected plates.

## Features

- Detects license plates using a trained YOLOv8 model.
- Extracts text from detected plates using EasyOCR.
- Applies multiple preprocessing techniques to improve OCR accuracy.
- Handles challenging conditions such as:
  - Low light
  - Blur
  - Glare
  - Skew
  - Noise
  - Varied angles
- Processes all images automatically from the `Testing/` folder.
- Saves annotated result images in the `output_results/` folder.
- Saves cropped plate images for inspection.
- Exports detection results to CSV.
- Displays OCR confidence, detection confidence, and processing time.

## Tech Stack

- Python
- OpenCV
- NumPy
- Pandas
- Matplotlib
- Ultralytics YOLOv8
- EasyOCR

## Project Structure

```bash
project/
├── Finalv.pt
├── Testing/
├── output_results/
├── requirements.txt
├── README.md

```

## Installation

Install the required dependencies:

```bash
pip install -r requirements.txt
```

If you are using a virtual environment, activate it first before installing the packages.

## Configuration

The project can be configured using the `CONFIG` dictionary in the code.

Important settings include:

- `model_path`: Path to the YOLOv8 model file.
- `testing_folder`: Folder containing input images.
- `output_dir`: Folder where results are saved.
- `image_exts`: Supported image file extensions.
- `conf_threshold`: Minimum confidence for detection.
- `iou_threshold`: IoU threshold for YOLO prediction.
- `ocr_languages`: Languages used by EasyOCR.
- `use_gpu`: Enables GPU acceleration if available.
- `resize_factor`: Upscaling factor used before OCR.
- `save_crops`: Saves detected plate crops.

## How It Works

1. Loads the trained YOLOv8 model from `Finalv.pt`.
2. Reads all images from the `Testing/` folder.
3. Detects license plates in each image using YOLOv8.
4. Crops each detected license plate.
5. Applies several preprocessing variants such as:
   - Low-light enhancement
   - Denoising
   - Deskewing
   - Sharpening
   - Glare removal
   - Adaptive thresholding
   - Morphological cleaning
6. Runs EasyOCR on all variants.
7. Selects the best OCR result using confidence-based voting.
8. Draws the detected plate text on the image.
9. Saves annotated images and cropped plates.
10. Exports all results to a CSV file.

## Usage

1. Place test images inside the `Testing/` folder.
2. Make sure the trained model file `Finalv.pt` is in the project directory.
3. Run the script or notebook.
4. Check the `output_results/` folder for:
   - Annotated result images
   - Cropped plate images
   - CSV output file

## Output Files

After execution, the following files are generated:

- `output_results/*_result.jpg` — annotated images with detection overlays.
- `output_results/crops/` — cropped license plate images.
- `output_results/detection_results.csv` — structured detection summary.

## Results Table

The exported results include:

- Image name
- Detected plate text
- OCR confidence
- Detection confidence
- Bounding box coordinates
- OCR processing time

## Notes

- EasyOCR may download its model automatically on first run.
- The pipeline is optimized for image-based plate detection.
- GPU support is disabled by default but can be turned on if needed.
- Results may vary depending on image quality and plate visibility.

## Future Improvements

- Add video input support.
- Improve text correction for region-specific plate formats.
- Add multilingual OCR support.
- Build a web interface or API for deployment.
