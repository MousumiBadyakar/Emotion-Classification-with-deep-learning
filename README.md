# Moodline – Emotion Classification with Deep Learning

**An instrument that reads the mood inside a sentence.**

Moodline is a deep learning-powered text emotion classification application that identifies the underlying emotion in a sentence. It uses a stacked Bidirectional GRU (BiGRU) neural network to classify text into six emotion categories and provides confidence scores for each prediction.

The project explores and compares different recurrent neural network architectures, including Simple RNN, LSTM, GRU, and Bidirectional GRU, before deploying the best-performing model through a FastAPI backend with an interactive web interface.

## Preview

Moodline provides a minimal, interactive interface where users can enter a sentence and instantly visualize its predicted emotion and probability distribution.

## Features

- **Six Emotion Categories:** Classifies text into Joy, Sadness, Love, Anger, Fear, and Surprise.
- **Deep Learning Model Comparison:** Experiments with Simple RNN, LSTM, GRU, and Bidirectional GRU architectures.
- **Bidirectional GRU:** Uses a stacked BiGRU architecture to capture contextual information from both directions.
- **Confidence Scores:** Displays the predicted emotion along with confidence scores for all six categories.
- **Text Preprocessing:** Cleans and tokenizes input text before passing it to the trained model.
- **Interactive Web Interface:** Provides a responsive interface built with HTML, CSS, and JavaScript.
- **REST API:** Exposes prediction and health-check endpoints through FastAPI.
- **Model Lifecycle Management:** Loads the trained model and tokenizer when the application starts.

## Tech Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Deep Learning | TensorFlow, Keras |
| NLP | Tokenization, Sequence Padding |
| Model Architectures | RNN, LSTM, GRU, BiGRU |
| Dataset | Hugging Face Datasets |
| Backend | FastAPI, Uvicorn |
| Frontend | HTML, CSS, JavaScript |
| Data Processing | NumPy |
| Deployment | Render |

## Dataset

The project uses the **Emotion Dataset** from Hugging Face.

Dataset: [dair-ai/emotion](https://huggingface.co/datasets/dair-ai/emotion)

It contains text samples categorized into six emotion labels:

| Label | Emotion |
|---|---|
| 0 | Sadness |
| 1 | Joy |
| 2 | Love |
| 3 | Anger |
| 4 | Fear |
| 5 | Surprise |

## Model Development

Four recurrent neural network architectures were explored and evaluated.

**1. Simple RNN**
- Embedding layer with 128-dimensional embeddings.
- Two SimpleRNN layers.
- Dropout regularization.

**2. Standard LSTM**
- Embedding layer with 128-dimensional embeddings.
- Two stacked LSTM layers.
- Dropout regularization.

**3. Standard GRU**
- Embedding layer with 128-dimensional embeddings.
- Two stacked GRU layers.
- Dropout regularization.

**4. Advanced Bidirectional GRU (Final Model)**
- 300-dimensional embedding layer.
- Two stacked Bidirectional GRU layers.
- GRU units: 128 and 64.
- Dropout regularization (0.5).
- Softmax output layer for six emotion classes.

The final BiGRU architecture was selected based on its performance during evaluation.

## Model Performance

Test accuracy comparison:

| Model | Test Accuracy |
|---|---:|
| Simple RNN | 14.95% |
| Standard GRU | 33.65% |
| Standard LSTM | 86.70% |
| **Bidirectional GRU** | **91.75%** |

The final Bidirectional GRU achieved **91.75% test accuracy** with a test loss of approximately 0.2203.

Additional evaluation includes confusion matrix visualization and sample predictions on unseen sentences.

## Project Structure

```text
Emotion-Classification-with-deep-learning/
│
├── Artifacts/
│   ├── BiGRU_Model.keras
│   └── tokenizer.pkl
│
├── static/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── Emotion Classification with deep learning.ipynb
├── main.py
├── requirements.txt
├── .python-version
└── README.md
```

## Installation and Setup

**1. Clone the repository**

```bash
git clone https://github.com/MousumiBadyakar/Emotion-Classification-with-deep-learning.git
```

**2. Navigate to the project directory**

```bash
cd Emotion-Classification-with-deep-learning
```

**3. Create a virtual environment**

```bash
python -m venv venv
```

**4. Activate the environment (Windows)**

```bash
venv\Scripts\activate
```

**5. Install dependencies**

```bash
pip install -r requirements.txt
```

**6. Run the FastAPI application**

```bash
uvicorn main:app --reload
```

The application will be available at:

```text
http://127.0.0.1:8000
```

## API Documentation

FastAPI automatically generates interactive API documentation.

- Swagger UI: `http://127.0.0.1:8000/docs`
- Health Check: `http://127.0.0.1:8000/health`

### Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Serves the Moodline web interface |
| GET | `/health` | Checks server and model loading status |
| POST | `/predict` | Predicts the emotion of input text |

### Emotion Prediction

**Request:**

```json
{
  "text": "I am so happy today!"
}
```

**Response:**

```json
{
  "text": "I am so happy today!",
  "predicted_emotion": "joy",
  "confidence": 0.849,
  "all_probabilites": {
    "sadness": 0.044,
    "joy": 0.849,
    "love": 0.007,
    "anger": 0.085,
    "fear": 0.011,
    "surprise": 0.003
  }
}
```

*Note: The response values above illustrate the expected format; actual probabilities depend on the input sentence.*

## Deployment

The application is configured for deployment on Render.

**Build Command:**

```bash
pip install -r requirements.txt
```

**Start Command:**

```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

The `.python-version` file specifies Python 3.11.11 for deployment compatibility with TensorFlow 2.17.0.

## Future Enhancements

- Improve classification performance across underrepresented emotion categories.
- Experiment with transformer-based architectures.
- Add batch text prediction.
- Enhance model interpretability and prediction explanations.
- Expand the application with multilingual emotion classification.

## Author

**Mousumi Badyakar**

---

*Moodline – Understanding the emotions behind your words.*