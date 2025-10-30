 GenAI LinkedIn Post Generator

This project is a LinkedIn Post Generator tool designed to help influencers create new posts that mimic their unique writing style.  
It analyzes a set of past posts to extract key characteristics and uses **Few-Shot Learning** with a **Large Language Model (LLM)** to generate new, contextually relevant content.

The application is built using **Streamlit** for the user interface and **LangChain** for orchestrating LLM calls, leveraging the **Groq API** for fast inference with the **Llama 3.2** model.


---

## ✨ Features

- **Custom Post Generation:** Generate posts based on selected topic, length (Short, Medium, Long), and language (English, Hinglish).  
- **Few-Shot Learning:** Automatically selects relevant past posts to provide the LLM with examples of the influencer’s writing style.  
- **Data Preprocessing:** Includes a script to enrich raw post data with metadata (line count, language, tags) and unify tags for better categorization.

---

## 🧠 Technical Architecture

The project follows a **two-stage architecture**:

### **Stage 1: Data Preprocessing (Offline)**  
1. Raw post data (`data/raw_posts.json`) is processed by `preprocess.py`.  
2. The LLM extracts metadata such as line count, language, and initial tags.  
3. A second LLM call unifies similar tags (e.g., *“Job Hunting”* and *“Jobseekers” → “Job Search”*).  
4. The enriched and categorized data is saved to `data/processed_posts.json`.

### **Stage 2: Post Generation (Online)**  
1. The Streamlit app (`main.py`) takes user input (Topic, Length, Language).  
2. `few_shot.py` filters `processed_posts.json` to find 1–2 matching examples.  
3. `post_generator.py` constructs a final prompt, including the user’s request and few-shot examples.  
4. The prompt is sent to the **Groq API (Llama 3.2)** to generate the new post.

---

## ⚙️ How It Works

This tool analyzes the posts of a LinkedIn influencer and helps them create new posts based on their past writing style.

For example, if **Mohan** is a LinkedIn influencer, he can feed his past posts to this tool. It will:
1. Extract key topics and stylistic patterns.  
2. Let him choose a topic, post length, and language.  
3. Generate a new post in his exact writing style with one click.
![tool](https://github.com/user-attachments/assets/c23b8b02-cdbb-4433-87df-0c89dc116874)


---

## 🧩 System Architecture Overview

**Stage 1:** Collect LinkedIn posts and extract Topic, Language, and Length.  
**Stage 2:** Use the extracted data to generate new posts, applying few-shot learning to replicate the writing style.

---![architecture](https://github.com/user-attachments/assets/3e31f217-fd7c-4199-b63f-9ce39e9c7ba2)


## 📁 Project Structure

| File/Directory | Description |
|----------------|-------------|
| `main.py` | Streamlit application entry point and UI layout. |
| `post_generator.py` | Core logic for prompt construction and LLM invocation. |
| `few_shot.py` | Handles loading and filtering of few-shot example data. |
| `llm_helper.py` | Initializes the ChatGroq client and loads the API key from `.env`. |
| `preprocess.py` | Script to enrich raw data and unify tags using the LLM. |
| `requirements.txt` | List of Python dependencies. |
| `data/` | Contains `raw_posts.json` and `processed_posts.json` (few-shot data). |
| `resources/` | Contains supporting images like `architecture.jpg` and `tool.jpg`. |
| `.env` | File to store the `GROQ_API_KEY`. |

---

## 🧰 Setup and Installation

### **Prerequisites**
- Python **3.10+**  
- A **Groq API Key** (obtain one from the [Groq Console](https://console.groq.com))

---

### **1. Clone the Repository**
```bash
git clone https://github.com/karen0133/Post-Generator-.git
cd project-genai-post-generator

### **2. Install Dependencies**
bash
Copy code
pip install -r requirements.txt
3. Configure API Key
Create a .env file in the root directory and add your Groq API key:

bash
Copy code
# .env
GROQ_API_KEY=YOUR_GROQ_API_KEY_HERE
Replace YOUR_GROQ_API_KEY_HERE with your actual key.

4. (Optional) Run Data Preprocessing
If you modify data/raw_posts.json or want to refresh the processed dataset, run:

bash
Copy code
python preprocess.py
This will regenerate data/processed_posts.json.

🚀 Usage
Run the Streamlit app:

bash
Copy code
streamlit run main.py
The app will launch in your browser at:

arduino
Copy code
http://localhost:8501
Select your topic, length, and language, then click Generate to create a new LinkedIn post in your style.

🧡 Credits
Developed using Streamlit, LangChain, and Groq Llama 3.2.

Inspired by the codebasics GenAI projects.

Special thanks to the open-source and AI communities for providing incredible tools and learning resources.


