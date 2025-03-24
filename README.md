# Custom LLM & Image-to-Text Application

This is a Flask-based web application that demonstrates two main features:

1. **Custom LLM Chat:**  
   A language model (LLM) that generates responses based on a provided topic. This model is trained on 2.7 billion parameters, delivering custom blog-style answers similar to conversational AI assistants.

2. **Image-to-Text OCR Integration:**  
   A feature that uses Tesseract OCR to extract text from uploaded images. The extracted text can be used as input to the language model, enabling users to generate content from visual inputs.

> **Note:**  
> The current frontend is minimal and functional, focusing on the core functionalities. Future improvements are planned to enhance the visual design and user experience.

## Features

- **LLM Chat Generation:**  
  Generate blog responses for various audiences (e.g., Professors, Students, or Common People) based on the topic and word count provided.

- **OCR Image Text Extraction:**  
  Upload an image to extract text using Tesseract OCR. This text can then be used as input to the language model for further processing.

- **Teacher Data Display:**  
  Displays a list of teachers fetched from a MySQL database.

- **User Authentication:**  
  Basic signup and login functionality to manage user sessions.

## Prerequisites

- **Python 3.7+**
- **MySQL Server:**  
  Ensure MySQL is installed and configured.
- **Tesseract OCR:**  
  - **Windows:** Download from [Tesseract at UB Mannheim](https://github.com/UB-Mannheim/tesseract/wiki) and verify the installation path (e.g., "C:\Program Files\Tesseract-OCR\tesseract.exe").
  - **macOS/Linux:** Install via your package manager (e.g., "brew install tesseract" or "sudo apt-get install tesseract-ocr").

## Installation

1. **Clone the Repository:**
   git clone https://github.com/yourusername/kite-education-app.git
   cd kite-education-app

2. **Create and Activate a Virtual Environment:**
   python -m venv venv
   source venv/bin/activate   (On Windows: venv\Scripts\activate)

3. **Install Dependencies:**
   pip install -r requirements.txt

## Large Model Binary Configuration

This project uses a custom LLM model binary (approx. 2.7GB) that is not included in the repository.

1. **Host the Model Externally:**  
   Upload the model binary to an external storage service (e.g., AWS S3, Google Cloud Storage, Dropbox, etc.) and obtain the download link.

2. **Environment Variable:**  
   Create a `.env` file in the project root and add the following line :
   LANGCHAIN_MODEL_URL=https://drive.google.com/file/d/1hm841OAK7I2MvK05ElE_A1YOmKCxgP20/view?usp=sharing

3. **Gitignore:**  
   Ensure any local copies of the binary are added to your `.gitignore` to avoid pushing them to GitHub.

4. **Loading the Model in Code:**  
   In `app.py`, read the environment variable using:
   import os
   model_url = os.getenv("LANGCHAIN_MODEL_URL")
   # Use model_url as needed for your LangChain configuration

## Database Setup

1. **Start MySQL Server** and log in:
   mysql -u root -p

2. **Create Database and Tables:**
   CREATE DATABASE llm;
   USE llm;

   CREATE TABLE signup (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       email VARCHAR(100) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL
   );

   CREATE TABLE teachers (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       email VARCHAR(100) UNIQUE NOT NULL,
       degree VARCHAR(100),
       work_experience INT
   );

3. **(Optional) Insert Sample Data:**
   INSERT INTO signup (name, email, password) VALUES
   ('John Doe', 'john@example.com', 'password123'),
   ('Jane Smith', 'jane@example.com', 'securepass');

   INSERT INTO teachers (name, email, degree, work_experience) VALUES
   ('Dr. Alice', 'alice@example.com', 'PhD in AI', 10),
   ('Prof. Bob', 'bob@example.com', 'MSc in Data Science', 7);

## Configuration

- **Tesseract OCR Path:**  
  In app.py, verify the following line reflects your Tesseract installation path:
  pyt.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"

- **LangChain Deprecation Notice:**  
  Warnings about deprecated imports from langchain may appear. Install the langchain-community package if needed:
  pip install -U langchain-community

## Running the Application

1. **Start the Flask Server:**
   python app.py

2. **Access the Application:**  
   Open your browser and go to http://127.0.0.1:5000/

## File Structure

kite-education-app/
├── app.py
├── database.py
├── requirements.txt
├── README.md
├── .env               # Contains LANGCHAIN_MODEL_URL and other configuration
└── templates/


## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Acknowledgements

- Flask: https://flask.palletsprojects.com/
- Tesseract OCR: https://github.com/tesseract-ocr/tesseract
- LangChain Community: https://github.com/langchain-ai/langchain
- Image resources from Unsplash (https://unsplash.com/) and Freepik (https://www.freepik.com/)
