Here is the revised version of your project documentation, including your repository URL:

---

# Video Classification and Refinement using OpenAI

This project processes a video file by extracting frames, transcribing audio, classifying the video, enhancing frames based on classification, and saving results. It utilizes OpenAI's API for classification and DALL-E 2 for image enhancements.

## Table of Contents

1. [Requirements](#requirements)
2. [Setup](#setup)
3. [Usage](#usage)
4. [Functions](#functions)
5. [Output](#output)
6. [IQA Metrics](#iqa-metrics)

## Requirements

To run this project, you need to have the following Python packages installed:

- `openai`
- `python-dotenv`
- `torch`
- `torchvision`
- `pandas`
- `numpy`
- `matplotlib`
- `imageio`
- `certifi`
- `opencv-python`
- `moviepy`
- `pillow`
- `natsort`
- `requests`

## Setup

1. **Clone the Repository**

   ```bash
   git clone https://github.com/titichayajojo/video_classification_refinement.git
   cd video_classification_refinement
   ```

2. **Create a Virtual Environment** (optional but recommended)

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure API Keys**

   Create a `.env` file in the root directory of the project with the following content:

   ```
   API_KEY=your_openai_api_key
   ```

## Usage

1. **Prepare Your Video**

   Place the video file you want to process in the `tedtalk/` directory. The script expects the video to be named `ted_1.mp4`, but you can adjust the path if needed.

2. **Run the Script**

   Execute the script with Python:

   ```bash
   python process_video.py
   ```

   This will:
   - Extract frames from the video at a specified interval.
   - Extract audio and transcribe it using OpenAI's Whisper model.
   - Classify the video into categories like Vox, TEDTalk, TaiChi, or MGIF.
   - Enhance the frames based on the classification using DALL-E 2.
   - Save the refined images and create a collage of the frames.

## Functions

### `process_video(video_path, seconds_per_frame=2)`

Extracts frames from the video and optionally extracts audio if available.

- **Parameters:**
  - `video_path` (str): Path to the input video.
  - `seconds_per_frame` (int): Interval for frame extraction.

- **Returns:**
  - `base64Frames` (list): List of base64 encoded frame images.
  - `audio_path` (str): Path to the extracted audio file (if available).

### `base64_to_image(base64_string)`

Converts a base64 encoded image string to an image binary buffer.

- **Parameters:**
  - `base64_string` (str): Base64 encoded image string.

- **Returns:**
  - `img_buffer` (BytesIO): Image binary buffer.

### `save_images(urls, base_path, target_width, target_height)`

Downloads and saves refined images from URLs to the specified path.

- **Parameters:**
  - `urls` (list): List of image URLs.
  - `base_path` (str): Path to save images.
  - `target_width` (int): Target width for resizing.
  - `target_height` (int): Target height for resizing.

### `create_horizontal_collage(image_paths, output_path, frame_count=7)`

Creates and saves a horizontal collage from the list of image paths.

- **Parameters:**
  - `image_paths` (list): List of paths to images.
  - `output_path` (str): Path to save the collage image.
  - `frame_count` (int): Number of frames to include in the collage.

## Output

- **Refined Images:** Saved in the `results/` directory, with each image named `image_{i}.png`.
- **Collage:** A collage of the images is saved as `collage.png` in the results directory.

## IQA Metrics

To evaluate the quality of the images before and after refinement, you can use Image Quality Assessment (IQA) metrics based on the BRISQUE (Blind/Referenceless Image Spatial Quality Evaluator) model. Refer to the [IQA BRISQUE GitHub repository](https://github.com/krshrimali/No-Reference-Image-Quality-Assessment-using-BRISQUE-Model?tab=readme-ov-file) for more details.

### Example Code for Running IQA

To calculate IQA scores for the original and refined frames, use the following commands:

1. **Calculate IQA for Original Frame**

   ```bash
   python3 brisquequality.py images/input/taichi/taichi_6/img_0.png
   ```

2. **Calculate IQA for Refined Frame**

   ```bash
   python3 brisquequality.py images/output/taichi/taichi_6/image_0.png
   ```

These commands will output the IQA scores for each image, helping you assess the improvement in image quality after the refinement process.

---
