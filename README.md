# TrainHub: Interactive Machine Learning Model Training Platform

TrainHub is a web-based platform that lets users upload datasets, configure machine learning models, and train them with customizable settings. With a Go backend managing user interactions and a Python backend handling ML tasks, TrainHub is designed to be fast, scalable, and easy to use. Users can experiment with algorithms, fine-tune parameters, and evaluate model performance—all through an intuitive interface.

---

## Features

1. **Dataset Upload and Management**
   - Upload datasets in CSV format and preview data with summary statistics.
   - Basic data preprocessing options like handling missing values and feature scaling.

2. **Model Selection and Configuration**
   - Choose from various algorithms (e.g., linear regression, decision trees, SVM).
   - Customize model parameters and set train-test split ratios.
   - Support for cross-validation and tuning.

3. **Model Training and Evaluation**
   - Asynchronous job handling for model training using Celery and Redis.
   - Display model performance metrics (accuracy, precision, F1 score) and visualizations.
   - Compare multiple models to find the best one for deployment.

4. **Model Deployment and API Integration**
   - Deploy trained models as REST API endpoints for real-time predictions.
   - Download models and view their parameters for reproducibility.

---

## Tech Stack

- **Backend**: Go (for API handling and frontend interactions), Python (for ML processing)
- **Machine Learning**: scikit-learn and Pandas in Python for model training and evaluation
- **Task Queue**: Redis and Celery for asynchronous ML task processing
- **Frontend**: HTML, CSS, JavaScript (or React for a more dynamic experience)
- **Database**: PostgreSQL or SQLite for storing dataset metadata, model configurations, and results

---

## Project Setup

### Prerequisites

- **Go** 1.16+
- **Python** 3.8+
- **Redis** (for task queue with Celery)
- **Node.js** (if using React for the frontend)

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/mush1e/TrainHub.git
   cd TrainHub
   ```

2. **Set Up Python Environment**:
   ```bash
   python3 -m venv ml_env
   source ml_env/bin/activate
   ```

3. **Install Python Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set Up Go Modules**:
   ```bash
   cd server
   go mod tidy
   ```

5. **Start Redis Server** (for Celery):
   ```bash
   redis-server
   ```

6. **Run Celery Worker**:
   ```bash
   celery -A ml_tasks worker --loglevel=info
   ```

7. **Start the Go Backend Server**:
   ```bash
   cd server
   go run main.go
   ```

8. **Start the Frontend**:
   - For a simple HTML/CSS/JavaScript frontend, open `frontend/index.html` in your browser.
   - If using React, navigate to the `frontend` directory and start the React app:
     ```bash
     cd frontend
     npm install
     npm start
     ```

---

## Usage

1. **Upload Dataset**: Use the `/upload` endpoint to upload CSV datasets.
2. **Select Model and Configure Parameters**: Choose an algorithm, configure hyperparameters, and set train-test split.
3. **Train Model**: Initiate model training. TrainHub processes training asynchronously, and you can view job status in real-time.
4. **View Results**: Access model metrics and visualizations like confusion matrices and ROC curves.
5. **Deploy Model**: Deploy your trained model as an API endpoint or download it for future use.

---

## Project Structure

```
TrainHub/
├── server/               # Go backend
│   ├── main.go           # Entry point for Go server
│   ├── handlers/         # HTTP handlers (file upload, API calls)
│   ├── tasks/            # Python task integration
├── ml_processing/        # Python scripts for model training
│   ├── train_model.py    # Core model training script
├── frontend/             # Frontend code
├── uploads/              # Folder for user-uploaded datasets
├── README.md
└── requirements.txt      # Python dependencies
```

---

## Sample API Workflow

1. **Dataset Upload**: Users upload a dataset via the Go backend’s `/upload` endpoint.
2. **Model Selection and Training**:
   - Go sends the dataset and configuration parameters to the Python backend through a task queue.
   - Python processes the task, training the model and calculating performance metrics.
3. **Results Retrieval**:
   - Once training is complete, results (metrics, charts, models) are available on the dashboard.
4. **Model Deployment**:
   - Trained models can be deployed as API endpoints for real-time predictions or downloaded for offline use.

---

## Contributing

1. Fork the repository and clone it to your local machine.
2. Create a branch for your feature: `git checkout -b feature-name`
3. Make your changes and commit them: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Future Enhancements

- **AutoML Feature**: Add an automated model and hyperparameter selection option.
- **Advanced Data Visualization**: Include more in-depth data visualizations like feature importance and pair plots.
- **Cloud Storage Integration**: Allow storage of larger datasets using cloud storage.
- **Additional ML Algorithms**: Add support for advanced algorithms and neural networks.

- 
