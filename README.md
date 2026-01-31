# EDA + Cleaning Pipeline (Demo Deploy)

This repo demonstrates a **deployable EDA/cleaning pipeline** executed via GitHub Actions.

## Quickstart
```bash
pip install -r requirements.txt
pip install -e .
python -m pipelines.run --config deploy/config.dev.yaml --input data/sample/dataset_sample.csv --output out_local --date 2026-01-31
```

## Deployment & Operations (GitHub Actions)
- **CI**: PRs run lint + tests + a smoke pipeline execution and publish artifacts
- **Scheduled runs**: weekly pipeline execution (`run-prod`) publishes reports and quality metrics
- **Artifacts**: each run uploads `eda_before_after.html` + `data_quality_metrics.json` + logs
