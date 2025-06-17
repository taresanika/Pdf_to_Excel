# PDF to Excel Resume Parser: Project Report

## 1. Problem Statement

In recruitment and human resource management, resumes are often received in PDF format, containing unstructured data such as candidate names, contact information, skills, work experience, projects, and extracurricular activities. Manually extracting and organizing this information into a structured format (e.g., Excel) is time-consuming, error-prone, and inefficient, especially when processing multiple resumes. The challenge is to develop an automated solution that extracts key information from PDF resumes and compiles it into a structured Excel file for efficient analysis and comparison.

## Features

- **Batch Processing**: Handles multiple PDF resumes at once.  
- **Structured Output**: Saves extracted data in an Excel file (`parsed_resume_data.xlsx`).  
- **Key Information Extraction**:  
  - Name (from the first 10 lines, excluding digits or emails).  
  - Email and phone number using regular expressions.  
  - Skills from a predefined list (e.g., Python, Java, SQL).  
  - Full sections for Experience, Projects, and Extra-Curricular activities.  
- **User-Friendly**: Simple file upload via Google Colab and automatic Excel download.

## Prerequisites

- Python 3.6+  
- Google Colab environment (for file upload/download functionality)  
- Required Python libraries:  
  - `pdfplumber`  
  - `spacy` (with `en_core_web_sm` model)  
  - `pandas`  
  - `openpyxl`  
  - `re` (for regular expressions)  


## 2. Objectives

The primary objectives of this project are:

- **Automate Data Extraction**: Develop a Python-based tool to extract relevant information (name, email, phone number, skills, experience, projects, and extracurricular activities) from PDF resumes.
- **Structured Output**: Convert the extracted data into a structured Excel file for easy access and analysis.
- **Scalability**: Ensure the solution can process multiple PDF resumes in a batch, saving time for recruiters.
- **Accuracy**: Implement robust text processing to accurately identify and extract key resume components.
- **User-Friendly**: Integrate a simple file upload mechanism for seamless interaction in a Google Colab environment.

## 3. Scope

### In-Scope:
- Extraction of specific resume fields: name, email, phone number, skills, work experience, projects, and extracurricular activities.
- Processing of PDF resumes uploaded via Google Colab.
- Use of natural language processing (NLP) and regular expressions for text extraction and parsing.
- Generation of an Excel file containing structured data from multiple resumes.
- Support for common resume formats with clearly labeled sections (e.g., "Experience," "Projects").

### Out-of-Scope:
- Handling non-PDF resume formats (e.g., Word, images).
- Advanced entity recognition beyond predefined fields (e.g., extracting specific job titles or company names).
- Processing resumes in languages other than English.
- Handling complex PDF layouts (e.g., multi-column or graphical resumes).
- Validation or verification of extracted data (e.g., checking email/phone validity).

## 4. Tools Used

- **Google Colab**: A cloud-based Jupyter notebook environment used for running the Python script, providing file upload and download capabilities.
- **Python**: The programming language used for developing the resume parser.
- **Jupyter Notebook**: The format (`Pdf_to_excel.ipynb`) used to structure and execute the code interactively.

## 5. Libraries Used

The following Python libraries were utilized to achieve the project objectives:

- **pdfplumber (v0.11.x)**: A library for extracting text from PDF files. It was used to read and extract text from resume PDFs page by page.
- **spacy (v3.x)**: A natural language processing library used for text processing. The `en_core_web_sm` model was employed for tokenization and text analysis.
- **pandas (v2.x)**: A data manipulation library used to create a DataFrame and export extracted data to an Excel file.
- **openpyxl (v3.x)**: A library for reading and writing Excel files, used in conjunction with pandas for Excel output.
- **re**: Python’s built-in regular expression library, used for extracting email addresses and phone numbers from resume text.
- **os**: A Python module for interacting with the file system, used to manage the upload folder and iterate through PDF files.
- **google.colab.files**: A Google Colab-specific module for handling file uploads and downloads in the notebook environment.

## 6. Methodology

### 6.1. Code Structure
The solution is implemented as a Jupyter notebook (`Pdf_to_excel.ipynb`) with the following key components:

1. **Dependency Installation**:
   - Installs required libraries (`pdfplumber`, `spacy`, `pandas`, `openpyxl`) using pip.
   - Downloads the SpaCy English model (`en_core_web_sm`) for text processing.

2. **File Upload and Storage**:
   - Creates a directory (`uploaded_resumes`) to store uploaded PDF files.
   - Uses `google.colab.files.upload()` to allow users to upload PDF resumes interactively.
   - Saves uploaded files to the `uploaded_resumes` directory.

3. **Text Extraction and Parsing**:
   - Defines a function `extract_info_from_text` to process resume text:
     - **Name Extraction**: Identifies the candidate’s name from the first 10 lines, excluding lines with digits, email symbols, or the word "experience."
     - **Email Extraction**: Uses a regular expression to find email addresses in the format `[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+`.
     - **Phone Number Extraction**: Uses a regular expression to match phone numbers in various formats (e.g., +123-456-7890, (123) 456-7890).
     - **Skills Extraction**: Searches for predefined technical skills (e.g., Python, Java, SQL) in the resume text, case-insensitive.
     - **Section Extraction**: Extracts full sections (Experience, Projects, Extra-Curricular) by identifying section headers and stopping at subsequent section titles.
   - The function returns a dictionary with extracted fields.

4. **Batch Processing**:
   - Iterates through all PDF files in the `uploaded_resumes` directory.
   - Uses `pdfplumber` to extract text from each PDF, page by page.
   - Applies the `extract_info_from_text` function to each resume’s text and stores the results in a list.

5. **Excel Generation**:
   - Converts the list of extracted data into a pandas DataFrame.
   - Saves the DataFrame to an Excel file (`parsed_resume_data.xlsx`) using `pandas.to_excel`.
   - Initiates automatic download of the Excel file using `google.colab.files.download`.

### 6.2. Assumptions
- Resumes are in English and follow a standard structure with identifiable section headers (e.g., "Experience," "Projects").
- PDFs contain extractable text (not scanned images or graphical resumes).
- Names appear in the top 10 lines and do not contain digits or email symbols.
- Skills are limited to a predefined list of technical keywords.

## 7. Limitations

- **Resume Format Dependency**: The code assumes resumes have clear section headers and text-based content. Multi-column or image-based PDFs may not be parsed correctly.
- **Name Extraction**: The heuristic for name extraction (first 10 lines, no digits or email symbols) may fail for unconventional resume formats.
- **Limited Skill Set**: Only predefined skills are extracted, potentially missing other relevant skills.
- **Language Support**: Only English resumes are supported due to the use of `en_core_web_sm`.
- **Error Handling**: The code lacks robust error handling for corrupted PDFs or missing sections.
- **Missing Import**: The code uses the `re` module for regular expressions but does not explicitly import it, which would cause an error unless added.

## 8. Recommendations for Improvement

- **Add Error Handling**: Implement try-catch blocks to handle corrupted PDFs or extraction failures gracefully.
- **Enhance Name Extraction**: Use SpaCy’s named entity recognition (NER) to identify names more accurately.
- **Expand Skill Extraction**: Incorporate a dynamic skill list or use NLP to identify skills not in the predefined list.
- **Support Complex PDFs**: Integrate OCR (e.g., using `pytesseract`) to handle scanned or image-based PDFs.
- **Multi-Language Support**: Add support for non-English resumes by using multilingual SpaCy models.
- **Validation**: Add checks to validate extracted emails and phone numbers.
- **Fix Missing Import**: Explicitly include `import re` in the code to ensure functionality.

## 9. Conclusion

The PDF to Excel Resume Parser successfully automates the extraction of key information from PDF resumes, converting unstructured data into a structured Excel format. By leveraging `pdfplumber` for PDF text extraction, `spacy` for text processing, and `pandas` for data organization, the solution achieves its objective of streamlining resume data processing. The tool is particularly effective for standard English resumes with clear section headers, making it valuable for recruiters handling multiple candidates. However, limitations in handling complex PDF formats and the lack of robust error handling highlight areas for future improvement. With minor enhancements, such as adding the missing `re` import and improving name extraction, the tool can become more robust and versatile for real-world recruitment workflows.
