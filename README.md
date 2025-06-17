PDF to Excel Resume Parser

A Python-based tool to extract key information from PDF resumes and save it as a structured Excel file. Built to run in Google Colab, this project automates the process of pulling out details like names, emails, phone numbers, skills, experience, projects, and extracurricular activities from multiple resumes.

Features





Batch Processing: Handles multiple PDF resumes at once.



Structured Output: Saves extracted data in an Excel file (parsed_resume_data.xlsx).



Key Information Extraction:





Name (from the first 10 lines, excluding digits or emails).



Email and phone number using regular expressions.



Skills from a predefined list (e.g., Python, Java, SQL).



Full sections for Experience, Projects, and Extra-Curricular activities.



User-Friendly: Simple file upload via Google Colab and automatic Excel download.

Prerequisites





Python 3.6+



Google Colab environment (for file upload/download functionality)



Required Python libraries:





pdfplumber



spacy (with en_core_web_sm model)



pandas



openpyxl



re (for regular expressions)

Installation





Clone the repository:

git clone https://github.com/your-username/pdf-to-excel-resume-parser.git
cd pdf-to-excel-resume-parser



Install dependencies:

pip install pdfplumber spacy pandas openpyxl



Download the SpaCy English model:

python -m spacy download en_core_web_sm

Usage





Open the Pdf_to_excel.ipynb notebook in Google Colab.



Run the first cell to install dependencies and download the SpaCy model.



Run the second cell to upload PDF resumes. A file picker will appear in Colab.



Run the remaining cells to:





Extract information from the uploaded PDFs.



Save the data to an Excel file (parsed_resume_data.xlsx).



Automatically download the Excel file.

Code Overview

The Jupyter notebook (Pdf_to_excel.ipynb) is structured as follows:





Dependency Setup: Installs libraries and downloads the SpaCy model.



File Upload: Creates an uploaded_resumes folder and saves uploaded PDFs.



Text Extraction: Uses pdfplumber to extract text from PDFs and a custom extract_info_from_text function to parse:





Name (heuristic-based from top 10 lines).



Email and phone number (via regex).



Skills (from a predefined list).



Sections (Experience, Projects, Extra-Curricular) by detecting headers.



Excel Output: Compiles data into a pandas DataFrame and exports it as an Excel file.

Note: The code assumes the re module is imported. Add import re to the notebook if not already present.

Example Output

The generated Excel file (parsed_resume_data.xlsx) contains columns:





file_name: Name of the PDF file.



name: Candidate's name.



email: Candidate's email address.



phone: Candidate's phone number.



skills: Comma-separated list of detected skills.



experience: Extracted Experience section text.



projects: Extracted Projects section text.



extra_curricular: Extracted Extra-Curricular section text.

Limitations





Works best with English resumes and clear section headers (e.g., "Experience").



Assumes PDFs contain extractable text (not scanned images).



Name extraction may fail for unconventional resume formats.



Skills are limited to a predefined list.



Lacks robust error handling for corrupted PDFs.

Future Improvements





Add OCR support for image-based PDFs using pytesseract.



Use SpaCy’s named entity recognition for better name extraction.



Expand skill detection beyond the predefined list.



Add multilingual support with SpaCy’s multilingual models.



Improve error handling for invalid or complex PDFs.

Contributing

Contributions are welcome! Please:





Fork the repository.



Create a feature branch (git checkout -b feature/your-feature).



Commit your changes (git commit -m "Add your feature").



Push to the branch (git push origin feature/your-feature).



Open a pull request.

License

This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgments





Built with pdfplumber, spacy, and pandas.



Designed for use in Google Colab.
