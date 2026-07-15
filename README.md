# 🚀 End-to-End Machine Learning Pipeline with DVC, Experiment Tracking & AWS S3

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)]()
[![DVC](https://img.shields.io/badge/DVC-Pipeline-orange.svg)]()
[![AWS](https://img.shields.io/badge/AWS-S3-yellow.svg)]()
[![GitHub](https://img.shields.io/badge/GitHub-Version%20Control-black.svg)]()

## 📌 Project Overview

This repository demonstrates how to build a **production-ready Machine Learning pipeline** using **DVC (Data Version Control)** for pipeline orchestration, **DVCLive** for experiment tracking, and **Amazon S3** as remote storage.

The project showcases industry-standard MLOps practices including:

- ✅ Modular ML pipeline
- ✅ Automated DVC pipelines
- ✅ Parameterized experiments
- ✅ Experiment tracking with DVCLive
- ✅ Data versioning
- ✅ Remote artifact storage using AWS S3
- ✅ Reproducible ML workflows

---

# 📂 Project Structure

```
.
├── data/
├── models/
├── reports/
├── src/
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_building.py
│   ├── model_evaluation.py
│   └── logger.py
├── dvc.yaml
├── params.yaml
├── requirements.txt
└── README.md
```

---

# ⚙️ Tech Stack

- Python 3.10
- DVC
- DVCLive
- AWS S3
- Git & GitHub
- Scikit-Learn
- YAML

---

# 🚀 Step 1: Build the ML Pipeline

### Clone the repository

```bash
git clone <repository-url>
cd <repository-name>
```

### Create the project structure

- Add the `src` folder
- Build each ML component individually:
  - Data Ingestion
  - Data Preprocessing
  - Feature Engineering
  - Model Building
  - Model Evaluation

### Ignore generated artifacts

Add the following folders to `.gitignore`

```
data/
models/
reports/
```

Commit your initial project.

```bash
git add .
git commit -m "Initial ML pipeline"
git push
```

---

# 🔄 Step 2: Build a DVC Pipeline

Initialize DVC

```bash
dvc init
```

Create a `dvc.yaml` file describing every stage of the ML workflow.

Run the pipeline

```bash
dvc repro
```

Visualize the pipeline DAG

```bash
dvc dag
```

Commit the generated DVC files

```bash
git add .
git commit -m "Added DVC pipeline"
git push
```

---

# ⚙️ Step 3: Parameterize the Pipeline

Create a `params.yaml` file.

Instead of hardcoding parameters, load them dynamically inside each pipeline stage.

Example:

```yaml
data_ingestion:
  test_size: 0.2

feature_engineering:
  max_features: 5000

model_building:
  random_state: 42
```

Reproduce the pipeline

```bash
dvc repro
```

Commit the changes

```bash
git add .
git commit -m "Parameterized pipeline"
git push
```

---

# 📊 Step 4: Track Experiments using DVCLive

Install DVCLive

```bash
pip install dvclive
```

Run experiments

```bash
dvc exp run
```

View all experiments

```bash
dvc exp show
```

Apply a previous experiment

```bash
dvc exp apply <experiment-name>
```

Delete an experiment

```bash
dvc exp remove <experiment-name>
```

Modify parameters inside `params.yaml` and execute another experiment.

Commit the experiment configuration.

---

# ☁️ Step 5: Configure AWS S3 as DVC Remote Storage

## Create AWS Resources

- Create an IAM User
- Create an S3 Bucket

Install dependencies

```bash
pip install dvc[s3]
pip install awscli
```

Configure AWS CLI

```bash
aws configure
```

Add S3 as the DVC remote

```bash
dvc remote add -d dvcstore s3://<bucket-name>
```

Push tracked files

```bash
dvc push
```

Commit the remote configuration

```bash
git add .
git commit -m "Configured S3 remote storage"
git push
```

---

# 📈 Loading Parameters from `params.yaml`

Create a reusable helper function.

```python
import yaml

def load_params(params_path: str) -> dict:
    with open(params_path, "r") as file:
        return yaml.safe_load(file)
```

Example usage inside pipeline stages.

### Data Ingestion

```python
params = load_params("params.yaml")
test_size = params["data_ingestion"]["test_size"]
```

### Feature Engineering

```python
params = load_params("params.yaml")
max_features = params["feature_engineering"]["max_features"]
```

### Model Building

```python
params = load_params("params.yaml")["model_building"]
```

This allows hyperparameters to be modified without changing the source code.

---

# 📊 DVCLive Integration

Import DVCLive

```python
from dvclive import Live
```

Log metrics and parameters during training.

```python
with Live(save_dvc_exp=True) as live:

    live.log_metric("accuracy", accuracy)

    live.log_metric("precision", precision)

    live.log_metric("recall", recall)

    live.log_params(params)
```

Every execution automatically creates a new DVC experiment, making model comparison simple and reproducible.

---

# 🧪 Useful DVC Commands

Initialize DVC

```bash
dvc init
```

Run pipeline

```bash
dvc repro
```

Show pipeline graph

```bash
dvc dag
```

Run experiment

```bash
dvc exp run
```

Show experiments

```bash
dvc exp show
```

Apply experiment

```bash
dvc exp apply <experiment-name>
```

Remove experiment

```bash
dvc exp remove <experiment-name>
```

Push artifacts to remote

```bash
dvc push
```

Pull artifacts

```bash
dvc pull
```

Check pipeline status

```bash
dvc status
```

---

# ⭐ Highlights

- Modular ML pipeline architecture
- Fully reproducible workflows using DVC
- Configurable pipelines with `params.yaml`
- Automated experiment tracking with DVCLive
- Remote artifact management using AWS S3
- Industry-standard MLOps workflow
- Easy collaboration through Git & GitHub

---

# 🤝 Contributing

Contributions, feature requests, and suggestions are welcome.

Feel free to fork the repository, open an issue, or submit a pull request.

---

# 📬 Connect

If you found this repository helpful, consider giving it a ⭐ on GitHub.

Happy Learning! 🚀
