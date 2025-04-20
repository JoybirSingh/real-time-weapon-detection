## Project Overview

This project implements a real-time weapon detection system that runs entirely in the browser by leveraging a YOLOv model exported to ONNX and executed via the Transformers.js library, eliminating the need for any backend server for inference. It uses a custom dataset of weapon images annotated with standard COCO class labels, organized into training, validation, and test splits for robust evaluation. The detection backbone is a YOLOv architecture fine-tuned for weapon recognition and optimized via ONNX Runtime to achieve high throughput on the client side.

## Features

- **Browser-Native Inference** using Transformers.js pipelines, handling preprocessing, model execution, and postprocessing seamlessly in JavaScript.  
- **YOLOv ONNX Model** exported with 16-bit precision (`model_fp16.onnx`) for reduced size and faster inference.  
- **Live Video Stream** capture from webcam, with bounding-box overlays drawn on a `<canvas>` in real time.  
- **Adjustable Parameters** for input size and detection threshold via slider controls, empowering users to trade off speed and accuracy.  

## Architecture

1. **Data Pipeline:** Images are preprocessed according to `preprocessor_config.json`, which rescales and resizes frames to the model’s expected input size.  
2. **Model Loading:** The ONNX model is fetched and instantiated in the browser using the Transformers.js ONNX Runtime backend.  
3. **Inference Loop:** A continuous loop captures video frames, passes them through the inference pipeline, and renders detections.  

## Prerequisites

- A modern web browser with WebGL/WebAssembly support.  
- An active webcam or video feed.  
- No additional server or runtime—purely client-side deployment.  

## Installation

```bash
# Clone the repo
git clone https://github.com/Lalman888/real-time-weapon-detection.git
cd real-time-weapon-detection

# Serve with any static file server, e.g. Python:
python3 -m http.server 8000
```

## Usage

1. Open `http://localhost:8000/index.html` in your browser.  
2. Grant camera access when prompted.  
3. Use the **Image size** and **Threshold** sliders to tune performance and confidence.  

## Dataset

The `dataset/` directory contains `train/`, `valid/`, and `test/` folders of annotated images, following the 80 COCO classes defined in `config.json`.

## Model

The repository includes `model/model_fp16.onnx`, a 16-bit quantized YOLOv model compatible with ONNX Runtime. To retrain or convert your own model, follow the steps in the YOLOv-ONNX examples.

## Configuration

- **`config.json`**: Maps COCO class IDs to labels and sets `model_type: "yolov"`.  
- **`preprocessor_config.json`**: Specifies normalization, resizing, and padding options for feature extraction.  

## Results

Early tests demonstrate detection of knives, pistols, and rifles at ~10–15 FPS on a mid-range laptop browser, with an average precision (AP) exceeding 75% on the validation set.

## Future Work

- Extend detection to additional weapon classes and real-world CCTV footage.  
- Integrate quantization techniques to further reduce model size and latency.  
- Add serverless logging of detections for analytics and alerts.  

## References

- Lalman888/real-time-weapon-detection repository  
- COCO Dataset: Microsoft Common Objects in Context  
- YOLOv ONNX & ONNXRuntime examples  
- YOLOv ONNX MIT (PyPI)  
- Transformers.js documentation  
- In-browser YOLOv & Transformers.js demo  
- Ultralytics ONNX export guide  
- Repository dataset structure  
- ONNX model file  
- Preprocessor settings  

---

**License:** MIT License (see `LICENSE` file for details)

