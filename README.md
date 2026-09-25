# Image Classifier Application

![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)

A lightweight Vue.js web application for running image classifiers on IIIF manifests or local images directly in the browser.

The application loads ONNX image-classification models, applies the corresponding preprocessing configuration, classifies IIIF canvases, and lets users export a filtered IIIF manifest containing the selected images and machine-generated annotations.

## Try a demo 

Test this app with a demo app on [![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-online-brightgreen?logo=github)](https://odil-ai.github.io/medieval-illumination-detector/)

## Features

- Load ONNX models from local artifacts or from Hugging Face.
- Classify all canvases in a IIIF manifest.
- Classify a single local image.
- Adjust the classification threshold.
- Reset the threshold to the model’s recommended value.
- Filter results by positive, negative, pending, error, or manually corrected items.
- Apply optional negative-label heuristics based on canvas labels.
- Correct model's suggestions
- Export the current filtered selection as a new IIIF Presentation API v3 manifest.
- Run entirely in the browser with no backend server.

## Limitations

For now this application is configure only for binary classification task.

## Configuration

The application is configured through `app.config.json`.

This file defines:

- the application mode: `local` or `online`;
- available model runs;
- labels and aliases;
- default IIIF manifest URL;
- project metadata;
- heuristic keywords;
- UI texts.

Example:

```json
{
  "mode": "online",
  "ui": {
    "title": "Medieval Illumination Detector",
    "defaultManifestUrl": "https://example.org/iiif/manifest.json"
  },
  "labels": {
    "positive": "illuminated",
    "negative": "non_illuminated"
  },
  "online": {
    "runs": [
      {
        "id": "mobilenetv3_large",
        "label": "MobileNet v3 large",
        "baseUrl": "https://huggingface.co/ORG/REPO/resolve/main/mobilenetv3_large"
      }
    ]
  }
}
```

Each model run should contain:

```
run/
├── onnx/
│   └── model.onnx
├── preprocess.json
└── inference_config.json
```

## Run locally

From the repository root:

```
python -m http.server 8000
```

Then open: `http://localhost:8000`

> Do not open index.html directly with file://, because browsers restrict local file access and CORS behavior.

## Citation

If you use this application in your work, please cite it using the metadata provided in [`CITATION.cff`](./CITATION.cff).
