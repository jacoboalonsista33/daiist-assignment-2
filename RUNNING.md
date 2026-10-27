# Solar Panel Assignment — Running the Project

## Dashboard

From this folder run:

```bash
uv sync --frozen
uv run python main.py app
```

Open http://127.0.0.1:7860. Upload a photograph, move both policy thresholds,
and use Restore to return to the validation-selected operating point.
The app loads weights/best.pt and artifacts; it does not train at startup.

## Training

```bash
uv run python main.py train
```

Settings are in pipeline_config.json. The pipeline uses api_key.py to download
susan-ifblr/panel-solar-bw945 version 1, preserves the original data, converts
polygons to enclosing boxes in a separate copy, trains YOLO11n, evaluates on
test, runs the unchanged COCO baseline, exports a predict-nothing baseline,
selects cost thresholds on validation, and saves dashboard artifacts.
On Colab retain GPU PyTorch and install dependencies with pip, not uv sync.
Provide ROBOFLOW_API_KEY through Secrets and the environment. Run
`!python main.py train` from the project folder.

Source and license: Susan, CC BY 4.0,
https://universe.roboflow.com/susan-ifblr/panel-solar-bw945/dataset/1

## Verification status

Six numerical and dataset-conversion tests passed with
`uv run python -m pytest -q`. The official `check.py` passed API verification,
weight loading, and dashboard HTTP startup. It does not retrain.
The weights and results are from the user's successful Colab notebook run.
The integrated train.py has not yet completed a new full training execution.
Before submission, run `!python check.py --train` on Colab to verify that stage.

## Still required before submission

- Write REPORT.md in your own words, with your own analysis and conclusions,
  identity fields, and AI-use disclosure. The original template is preserved.
- Justify hypothetical economic assumptions and separately dimension incident
  handling staff. The app's staff equivalent covers photo review only.
- Explain absent bird_drop test cases, class imbalance, the exact duplicate,
  possible near-duplicates, and indoor images versus production conditions.
- Complete the final integrated training verification on Colab.
- Push to the fork, open the assignment PR, and submit its URL and ZIP.

The dashboard is a decision simulation; it creates no external tickets.
Pass is not a healthy-panel certification. Confidence is not a calibrated
probability. Costs assume perfect human review and 10% production prevalence.
Actual split counts and prevalence-adjusted expected counts are labeled
separately. Missing test-class metrics are N/A, not zero.

This project archive excludes .env and other local runtime files.
