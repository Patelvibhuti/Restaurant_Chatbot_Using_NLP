# 🍽️ Restaurant Chatbot Using NLP (Foodmonger's Restro)

> A smart NLP-powered restaurant chatbot built with **FastText embeddings**, **Cosine Similarity-based Intent Classification**, and **Flask**. The bot automates customer interactions including table bookings, menu browsing, chef recommendations, feedback collection, and more.

---

## 📌 Overview

This project implements a conversational AI chatbot for a restaurant named **"Foodmonger's Restro"**. The chatbot understands natural language user queries, classifies their intent, and responds appropriately — whether it's showing menu items, booking a table, telling a joke, or handling customer feedback.

The system uses **FastText pre-trained word embeddings** (`cc.en.300.bin`) to convert sentences into 300-dimensional vectors. Intent classification is performed using **cosine similarity** between the user's input vector and pre-embedded intent pattern vectors. Responses are either static, dynamically fetched from **MongoDB** (menu, bookings, feedback), or context-aware (e.g., day-based offers and chef suggestions).

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 💬 **Greetings & Identity** | Welcomes users and introduces itself as "Foodmonger" |
| 📅 **Table Booking** | Books tables with a unique UUID, tracks real-time seat availability |
| 🍕 **Menu Browsing** | Browse items by category (Soup, Chinese, Pizza, Indian Main Course, Rice, Breads, Dal, Chaat, South Indian, Dessert) and dietary preference (Veg / Non-Veg) |
| 👨‍🍳 **Chef Recommendations** | Suggests dishes based on the current day of the week |
| 🏷️ **Daily Offers** | Displays rotating offers based on the day |
| 📝 **Feedback Collection** | Records positive and negative feedback into MongoDB |
| 📍 **Contact & Address** | Shares restaurant location, email, and helpline |
| 🏥 **Sanitation Info** | Explains COVID-19 safety protocols |
| 😂 **Jokes** | Cracks food-related jokes to entertain customers |
| 📊 **t-SNE Visualization** | Visualizes intent clusters in 2D using t-SNE |

---

## 🏗️ System Architecture

```
┌──────────────┐      ┌─────────────────┐      ┌──────────────────────┐
│   User       │──────▶  Flask Web App  │──────▶  Intent Classifier   │
│  (Browser)   │      │    (app.ipynb)  │      │ (intent_classifier)  │
└──────────────┘      └─────────────────┘      └──────────────────────┘
                              │                           │
                              │                    FastText Embeddings
                              │                    Cosine Similarity
                              ▼                           ▼
                     ┌─────────────────┐      ┌──────────────────────┐
                     │   Frontend UI   │      │  Response Generator  │
                     │ (HTML/CSS/JS)   │◀─────│ (Response_generator) │
                     └─────────────────┘      └──────────────────────┘
                                                        │
                          ┌──────────────┬──────────────┼──────────────┐
                          ▼              ▼              ▼              ▼
                    ┌─────────┐    ┌─────────┐   ┌──────────┐   ┌─────────┐
                    │ MongoDB │    │dataset. │   │embedded_ │   │Static   │
                    │Database │    │  json   │   │ data.json│   │Responses│
                    └─────────┘    └─────────┘   └──────────┘   └─────────┘
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Python 3.x** | Core programming language |
| **Flask** | Lightweight web framework for serving the chatbot UI and API |
| **Jupyter Notebooks** | Development environment for all modules |
| **FastText** | Pre-trained word embeddings (`cc.en.300.bin`) |
| **MongoDB** | NoSQL database for menu, bookings, and feedback |
| **NLTK** | Text preprocessing (tokenization, lemmatization) |
| **NumPy** | Numerical operations and vector math |
| **scikit-learn** | t-SNE visualization and K-Means clustering |
| **yellowbrick** | Enhanced t-SNE visualization |
| **HTML / CSS / JavaScript** | Frontend chat interface |
| **jQuery** | AJAX calls for real-time chat |
| **import-ipynb** | Import Jupyter notebooks as Python modules |

---

## 📁 Project Structure

```
Restaurant_Chatbot_Using_NLP/
│
├── app.ipynb                          # Flask web application entry point
├── intent_classifier.ipynb            # Intent classification using cosine similarity
├── Response_generator.ipynb           # Generates responses based on detected intent
├── Data_embedder.ipynb                # Embeds dataset patterns using FastText
├── sentence_normalizer.ipynb          # Text preprocessing pipeline
├── fast_text.ipynb                    # FastText model download & preparation
├── tsne_visualizer.ipynb              # t-SNE visualization of intent clusters
├── training_data.txt                  # Minimal training data samples
│
├── Dataset/
│   ├── dataset.json                   # Intent patterns & responses (training data)
│   ├── embedded_data.json             # FastText-embedded intent patterns (generated)
│   ├── embedded_data_short.json       # Subset for t-SNE visualization
│   └── menu.json                      # Restaurant menu items with prices & categories
│
├── static/
│   └── images/
│       ├── logo.png                   # Restaurant logo
│       └── slider.jpg                 # Background image for chat UI
│
├── templates/
│   ├── index.html                     # Main chat interface
│   ├── styles.css                     # Chat UI styling
│   └── script.js                      # Frontend chat logic (AJAX)
│
└── README.md                          # You are here!
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:
- **Python 3.7+**
- **MongoDB** (running locally on `localhost:27017`)
- **pip** (Python package manager)
- **Jupyter Notebook / JupyterLab**

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/RestaurantChatbotUsingNLP.git
   cd RestaurantChatbotUsingNLP
   ```

2. **Install required Python packages:**
   ```bash
   pip install flask pymongo fasttext numpy nltk scikit-learn yellowbrick import-ipynb
   ```

3. **Download NLTK data (if needed):**
   ```python
   import nltk
   nltk.download('wordnet')
   nltk.download('omw-1.4')
   ```

4. **Start MongoDB:**
   Make sure your MongoDB server is running locally:
   ```bash
   mongod
   ```

### Running the Chatbot

Follow these steps in order:

#### Step 1: Prepare the FastText Embedding Model
Open and run `fast_text.ipynb`. This downloads the English FastText model (`cc.en.300.bin`) if not already present.

#### Step 2: Generate Embeddings for Training Data
Open and run `Data_embedder.ipynb`. This:
- Loads `dataset.json`
- Normalizes all intent patterns using `sentence_normalizer`
- Embeds them using FastText
- Saves the result as `Dataset/embedded_data.json`

#### Step 3: Launch the Flask Application
Open and run `app.ipynb`. This starts the Flask server (usually on `http://127.0.0.1:5000/`).

#### Step 4: Chat with the Bot!
Open your browser and navigate to the local server URL. Start chatting with **Foodmonger**!

---

## 🧠 How the NLP Pipeline Works

### 1. Sentence Normalization (`sentence_normalizer.ipynb`)
Raw user input is cleaned before embedding:
- **Lowercasing** everything
- **Tokenization** using `RegexpTokenizer(r'\w+')`
- **Lemmatization** (verbs) using WordNetLemmatizer
- **Stopword removal** (custom list: the, you, i, are, is, a, me, to, can, etc.)

```python
# Example: "I'd like to order some pizza!"
# → "would like order some pizza"
```

### 2. Sentence Embedding (`Data_embedder.ipynb`)
Uses FastText's `get_sentence_vector()` to convert a normalized sentence into a 300-dimensional vector.

### 3. Intent Classification (`intent_classifier.ipynb`)
- Loads pre-embedded patterns from `embedded_data.json`
- Computes **cosine similarity** between user input vector and each pattern vector
- Returns the intent `tag` with highest similarity
- **Tie-breaking:** If multiple intents tie, compares the average of top-4 scores
- **Thresholds:** If max similarity < 0.6 (or average < 0.06 for ties), returns empty tag → fallback response

### 4. Response Generation (`Response_generator.ipynb`)
Maps the detected intent tag to a response function:

| Intent Tag | Action |
|------------|--------|
| `greeting` | Returns a random greeting message |
| `book_table` | Decrements seat count, generates booking UUID, stores in MongoDB |
| `available_tables` | Returns current available seat count |
| `menu` | Lists all menu items from MongoDB |
| `veg_soup`, `nonveg_soup`, `veg_chinese`, etc. | Queries MongoDB by category & dietary flag |
| `suggest` | Returns day-specific chef recommendations |
| `offers` | Returns day-specific promotional offers |
| `positive_feedback` / `negative_feedback` | Saves feedback text to MongoDB |
| `contact` / `address` / `hours` | Returns static restaurant info |
| `jokes` | Returns a random food joke |
| `general` | Returns generic fallback responses |

---

## 🗄️ Dataset Description

### `Dataset/dataset.json`
Contains chatbot training data in the following format:
```json
{
  "intents": [
    {
      "tag": "greeting",
      "patterns": ["Hi", "Hello", "Good morning!"],
      "responses": ["Hello I'm Foodmonger! How can I help you?"]
    },
    {
      "tag": "book_table",
      "patterns": ["Book a table", "Can I reserve a seat?"],
      "responses": [""]
    }
  ]
}
```
There are **30+ intents** covering greetings, menu queries, bookings, feedback, jokes, and more.

### `Dataset/menu.json`
Contains restaurant menu items:
```json
[
  {
    "item_id": "001",
    "item": "Tomato soup",
    "cost": 150,
    "veg": "Y",
    "Non veg": "N",
    "category": "Soup"
  }
]
```
Categories include: **Soup, Chaat, Chinese, Pizza, Indian Main Course, Breads, Dal, Rice, South Indian, Dessert**.

### `Dataset/embedded_data.json`
Generated file containing the same structure as `dataset.json`, but with `patterns` replaced by their 300-dimensional FastText vectors.

---

## 🔌 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Serves the chatbot frontend (`index.html`) |
| `/get?msg=<user_message>` | GET | Returns the chatbot's text response |

### Example API Call
```bash
curl "http://127.0.0.1:5000/get?msg=Show%20me%20veg%20pizza"
# Response: "Veg Pizza options are: Italian Pizza for Rs. 210, Mexican Pizza for Rs. 250, ..."
```

---

## 💬 Usage Examples

| User Input | Bot Response |
|------------|--------------|
| "Hello" | "Hello I'm Foodmonger! How can I help you?" |
| "Book a table" | "Your table has been booked successfully. Please show this Booking ID at the counter: `abc-123-xyz`" |
| "How many tables are available?" | "There are 69 table(s) available at the moment." |
| "Show me veg soup" | "Veg Soup options are: Tomato soup for Rs. 150, Lemon coriander soup for Rs. 120, ..." |
| "What do you recommend?" | "Chef recommends: For Veg - Hyderabadi Masala Dosa, Dahi wada :::: For non veg - Chicken Fried rice, Chicken Tikka Masala" |
| "Any offers today?" | "Buy any 3 south indian dish and get 1 free" (Wednesday) |
| "Tell me a joke" | "A red curry and a green curry had a fight, there was no winner it was Thai" |
| "I loved the food" | "Thank you so much for your valuable feedback. We look forward to serving you again!" |

---

## 📝 Important Notes

- **MongoDB Connection:** The chatbot expects MongoDB running at `mongodb://localhost:27017/`. The database name is `restaurant` with collections: `menu`, `feedback`, `bookings`.
- **Absolute Paths:** Some notebooks historically used hardcoded Windows paths. These have been fixed per the `TODO.md` (ensure you use relative paths for cross-platform compatibility).
- **import-ipynb:** This project uses `import_ipynb` to import other notebooks as modules. Ensure it is installed.
- **Seat Count:** Table availability is managed by a global `seat_count` variable initialized to 70 (not persisted to DB).
- **First Run:** You must run `Data_embedder.ipynb` at least once to generate `embedded_data.json` before starting the Flask app.

---

## 🔮 Future Scope

The chatbot currently demonstrates a solid rule-based + similarity NLP pipeline. However, several enhancements can significantly improve its intelligence, scalability, and user experience:

### 1. Advanced NLP Models
Replace the current **cosine-similarity + FastText** approach with modern deep learning architectures such as:
- **BERT / DistilBERT** for contextual intent classification
- **RNNs (LSTM/GRU)** or **Transformers** for sequence understanding
- Fine-tuning on domain-specific restaurant conversation datasets

### 2. Conversational Context & Memory
- Implement **multi-turn dialogue handling** so the bot remembers previous user inputs within a session (e.g., "Show me veg pizza" → "Which one is cheapest?")
- Add **slot filling** for incomplete booking queries (date, time, number of guests)

### 3. Deployment & DevOps
- **Dockerize** the entire stack (Flask + MongoDB) for one-click deployment
- Deploy on **cloud platforms** (AWS, GCP, Azure) or **Heroku**
- Add **CI/CD pipelines** (GitHub Actions) for automated testing and deployment

### 4. Voice & Multilingual Support
- Integrate **Speech-to-Text (STT)** and **Text-to-Speech (TTS)** for hands-free interaction
- Add **multilingual support** (Hindi, Gujarati, etc.) using multilingual FastText or mBERT

### 5. Admin Dashboard & Analytics
- Build a **web-based admin panel** to:
  - View table bookings and availability in real-time
  - Analyze customer feedback sentiment trends
  - Update menu items and prices dynamically
  - Monitor chatbot conversation logs and intent accuracy

### 6. Order Placement & Payment Integration
- Allow users to **place actual orders** through the chatbot
- Integrate **payment gateways** (Razorpay, Stripe, PayPal)
- Generate **digital invoices** and send order confirmations via email/SMS

### 7. Improved Recommendation Engine
- Move beyond day-based static recommendations to **personalized suggestions** using:
  - User order history
  - Popular/trending dishes
  - Collaborative filtering or content-based recommendation algorithms

### 8. Code Refactoring & Testing
- Convert all `.ipynb` notebooks into **proper `.py` modules** for production readiness
- Add **unit tests** (pytest) and **integration tests** for all components
- Implement **logging** and **error tracking** (Sentry, Loguru)

### 9. Mobile Application
- Develop a **React Native / Flutter** mobile app for iOS and Android
- Enable **push notifications** for order updates, offers, and booking reminders

### 10. Sentiment Analysis Enhancement
- Use **fine-grained sentiment analysis** (positive, negative, neutral, mixed) on feedback
- Automatically escalate highly negative feedback to restaurant management

---


<p align="center">Made with ❤️ and 🍕 for Foodmonger's Restro</p>

