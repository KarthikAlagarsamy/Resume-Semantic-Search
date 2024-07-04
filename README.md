# Resume Semantic Search with BERT Embeddings

## Introduction

The code leverages the BERT model and the Gradio library to create a semantic search tool for resumes. The primary purpose of this tool is to allow users to input job descriptions or queries and a list of resume URLs, and then return the top resumes that best match the queries based on semantic similarity.

## Libraries and Tools
Several libraries and tools are used in this project:
•	Gradio: A Python library that makes it easy to create interactive user interfaces for machine learning models.
•	Transformers: A library by Hugging Face that provides state-of-the-art machine learning models including BERT.
•	PyPDF2: A library for reading PDF files.
•	BeautifulSoup: A library for web scraping purposes to extract text from HTML.
•	Requests: A library for making HTTP requests to fetch content from the web.

## Steps Involved
### 1. Installation of Packages
The necessary packages are installed using pip. This includes Gradio, Transformers, PyPDF2, BeautifulSoup, and Requests.
### 2. Model Initialization
The BERT model (bert-base-uncased) and its tokenizer are initialized. BERT (Bidirectional Encoder Representations from Transformers) is a transformer-based model designed for natural language understanding.
### 3. Extracting Text from PDFs
The function extract_text_from_pdf_url(pdf_url) is responsible for fetching a PDF from a URL, saving it locally, and then extracting the text from each page using PyPDF2. If the HTTP request to fetch the PDF fails, an error message is printed.
### 4. Fetching Resume Text from HTML
The function fetch_resume_from_url(url) fetches the content of a webpage, parses it with BeautifulSoup, and extracts the text. This function is useful for processing resumes that are available as web pages instead of PDFs.
### 5. Generating BERT Embeddings
The function generate_embeddings(text) tokenizes the input text and generates embeddings using the BERT model. It returns the mean of the last hidden state of BERT's output as the embedding for the text.
### 6. Preprocessing Resume Text
The function preprocess_resume(text) divides the resume text into different sections: work experience, education, and skills. It uses keywords to identify and split these sections. The text is converted to lowercase for keyword matching. If any section is not found, it is left empty.
### 7. Searching Resumes
The core function search_resumes(queries, resume_urls) processes the input queries and resume URLs. It performs the following steps:
•	Splits the input queries and resumes into separate lines.
•	For each query, generates an embedding using the generate_embeddings function.
•	For each resume URL, fetches the resume text using extract_text_from_pdf_url or fetch_resume_from_url.
•	Preprocesses the resume text into sections using preprocess_resume.
•	Generates embeddings for each section of the resume.
•	Combines these embeddings (using a simple average) to create a single embedding for the entire resume.
•	Computes the cosine similarity between the query embedding and the resume embedding.
•	Stores the similarity score and resume details in a list.
After processing all queries and resumes, the results are sorted based on similarity scores in descending order. The top results are then formatted into a string for display.
### 8. Gradio Interface
The Gradio interface is defined with two input text boxes for queries and resume URLs, and one output text box for displaying the top resumes. The search_resumes function is linked to the Gradio interface, allowing users to interactively perform resume searches based on their queries.

## Conclusion
This project demonstrates the use of advanced NLP models and interactive interfaces to solve practical problems like resume searching. By leveraging BERT embeddings, the tool can understand the semantic meaning of the text, providing more accurate and relevant results compared to traditional keyword-based search methods. The integration with Gradio makes it user-friendly and easily accessible.

