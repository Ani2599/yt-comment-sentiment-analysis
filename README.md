# YT Chrome Plugin for Sentiment Analysis of YouTube Comments

This project is a Chrome plugin that performs sentiment analysis on YouTube comments, offering insights into the general tone (positive, neutral, or negative) of comments on videos. The project combines machine learning, cloud services, experiment tracking, and deployment automation, using tools like MLflow, LightGBM, AWS, Flask, Docker, and GitHub Actions for continuous integration and delivery.

## Project Structure

- **Data Source**: The comment data is stored in a CSV file.
- **Experiment Tracking**: MLflow is hosted on an EC2 instance to track experiments and model performance metrics.
- **Model Selection**: Several classification models were tested, and LightGBM was selected as the final model for deployment.
- **Version Control**: Git is used for code versioning, and DVC (Data Version Control) is used to manage and version the dataset. The dataset is stored in an AWS S3 bucket.
- **API Development**: A Flask API is created to serve the model's predictions, which are consumed by the Chrome extension.
- **Frontend**: The Chrome extension is in a separate repository (`yt-chrome-plugin-frontend`). It includes files like `popup.js`, `popup.html`, and `manifest.json`.
- **Containerization**: Docker is used to containerize the application.
- **Deployment**: 
  - **Docker Image Storage**: The Docker image is stored in AWS Elastic Container Registry (ECR).
  - **Deployment**: AWS CodeDeploy is used to deploy the application, with a CI/CD pipeline automated through GitHub Actions.

## Features

- **Sentiment Prediction**: Analyze comments on YouTube videos to determine if they are positive, neutral, or negative.
- **Visualization**: Generates sentiment distribution charts and word clouds to give visual insights into comment sentiment.
- **Trend Analysis**: Displays a trend graph for sentiment changes over time.
- **Chrome Plugin Integration**: Provides a user-friendly interface on YouTube for instant sentiment analysis of comments.

## Installation

### Prerequisites

- Python 3.7+
- Docker
- AWS account (for ECR, S3, and CodeDeploy)
- Git and DVC
- Chrome browser for testing the plugin

### Steps

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/your-username/yt-chrome-plugin.git
    cd yt-chrome-plugin
    ```

2. **Setup Environment**:
    - Install Python dependencies:
      ```bash
      pip install -r requirements.txt
      ```
    - Configure AWS credentials for Docker and S3 access.

3. **Run Flask API Locally**:
    ```bash
    python app.py
    ```
    The API should be running at `http://localhost:5000`.

4. **Build and Push Docker Image**:
    - Build the Docker image:
      ```bash
      docker build -t yt-sentiment-analysis .
      ```
    - Tag and push the image to AWS ECR.

5. **Deploy Using CodeDeploy**:
    - Configure and trigger deployment through AWS CodeDeploy.
    - Set up the CI/CD pipeline with GitHub Actions for automated deployment.

## API Endpoints

- **GET /**: Home route to check if the server is running.
- **POST /predict**: Predict sentiment for a batch of comments.
- **POST /predict_with_timestamps**: Predict sentiment with timestamps for trend analysis.
- **POST /generate_chart**: Generate a pie chart for sentiment distribution.
- **POST /generate_wordcloud**: Generate a word cloud from comments.
- **POST /generate_trend_graph**: Generate a trend graph for sentiment over time.

## Testing

Testing is performed to ensure the following:
- **Model Loading**: Verifies that the correct model is loaded from the registry.
- **Model Performance**: Tests model accuracy, precision, and recall.
- **Model Signature**: Ensures the model input/output signature matches expectations.
- **API Functionality**: Validates Flask API endpoints for response correctness.
- **Deployment**: Checks for successful deployment using Docker and CodeDeploy.

## Chrome Plugin

The Chrome extension is stored in a separate repository, [yt-chrome-plugin-frontend](https://github.com/your-username/yt-chrome-plugin-frontend). It includes:
- **popup.js**: JavaScript logic for plugin functionality.
- **popup.html**: HTML for the plugin UI.
- **manifest.json**: Metadata and permissions for the Chrome extension.

To install the extension:
1. Go to Chrome Extensions.
2. Enable **Developer mode**.
3. Click **Load unpacked** and select the `yt-chrome-plugin-frontend` folder.

## Technologies Used

- **Machine Learning**: LightGBM, NLP preprocessing with NLTK
- **API**: Flask
- **Cloud Services**: AWS S3, ECR, CodeDeploy, EC2 (MLflow server)
- **Version Control**: Git and DVC
- **Containerization**: Docker
- **CI/CD**: GitHub Actions

## Authors

- **Aniket**

## License

This project is licensed under the MIT License - see the LICENSE file for details.

