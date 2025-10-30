GenAI LinkedIn Post Generator
This project is a LinkedIn Post Generator tool designed to help influencers create new posts that mimic their unique writing style. It analyzes a set of past posts to extract key characteristics and uses Few-Shot Learning with a Large Language Model (LLM) to generate new, contextually relevant content.

The application is built using Streamlit for the user interface and LangChain for orchestrating LLM calls, leveraging the Groq API for fast inference with the Llama 3.2 model.

Features
Custom Post Generation: Generate posts based on selected topic, length (Short, Medium, Long), and language (English, Hinglish).
Few-Shot Learning: Automatically selects relevant past posts to provide the LLM with examples of the influencer’s writing style.
Data Preprocessing: Includes a script to enrich raw post data with metadata (line count, language, tags) and unify tags for better categorization.
Technical Architecture
The project follows a two-stage architecture:

Stage 1: Data Preprocessing (Offline)
Raw post data (data/raw_posts.json) is processed by preprocess.py.
The LLM extracts metadata such as line count, language, and initial tags.
A second LLM call unifies similar tags (e.g., “Job Hunting” and “Jobseekers” → “Job Search”).
The enriched and categorized data is saved to data/processed_posts.json.
Stage 2: Post Generation (Online)
The Streamlit app (main.py) takes user input (Topic, Length, Language).
few_shot.py filters processed_posts.json to find 1–2 matching examples.
post_generator.py constructs a final prompt, including the user’s request and few-shot examples.
The prompt is sent to the Groq API (Llama 3.2) to generate the new post.
How It Works
This tool analyzes the posts of a LinkedIn influencer and helps them create new posts based on their past writing style.

For example, if Mohan is a LinkedIn influencer, he can feed his past LinkedIn posts to this tool. It will extract key topics and let him choose a topic, post length, and language. After clicking Generate, it creates a new post that matches Mohan’s writing style.

Tool Preview

System Architecture Overview
System Architecture

Stage 1: Collect LinkedIn posts and extract Topic, Language, and Length.
Stage 2: Use the extracted data to generate new posts, applying few-shot learning to replicate the writing style.
Project Structure
File/Directory	Description
main.py	Streamlit application entry point and UI layout.
post_generator.py	Core logic for prompt construction and LLM invocation.
few_shot.py	Handles loading and filtering the few-shot example data.
llm_helper.py	Initializes the ChatGroq client and loads the API key from .env.
preprocess.py	Script to enrich raw data and unify tags using the LLM.
requirements.txt	List of Python dependencies.
data/	Contains raw_posts.json and processed_posts.json (the few-shot data).
resources/	Contains supporting images like architecture.jpg and tool.jpg.
.env	File to store the GROQ_API_KEY.
Setup and Installation
Prerequisites
Python 3.10+
A Groq API Key (obtain one from Groq Console)
1. Clone the Repository
git clone https://github.com/Gesare-n/Post-Generator-.git cd project-genai-post-generator

2. Install Dependencies
Install the required Python packages using pip:

pip install -r requirements.txt

3. Configure API Key
Create a .env file in the root of the project directory and add your Groq API key:

.env file
GROQ_API_KEY=YOUR_GROQ_API_KEY_HERE

Replace YOUR_GROQ_API_KEY_HERE with your actual Groq API key.

4. (Optional) Run Data Preprocessing
If you modify data/raw_posts.json or want to refresh the processed dataset, run:

python preprocess.py

This will regenerate data/processed_posts.json.

Usage
Run the Streamlit app:

streamlit run main.py

The application will launch in your default browser at:

http://localhost:8501

Select your topic, length, and language, then click Generate to create a new LinkedIn post in your style.
