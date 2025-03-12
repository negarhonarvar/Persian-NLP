# Persian Effective Unit Extractor

This repository contains a complete pipeline for extracting the **minimal set of effective units** from Persian text. The project includes all major steps from PDF extraction, preprocessing, morphological segmentation, minimal set extraction, and verb simplification—all implemented using open-source libraries.

---

## Overview

The goal of this project is to process a Persian text PDF and produce a CSV file containing a minimal collection of *effective units* (meaningful tokens) that meet the following criteria:

- **No redundancy:** Each effective unit appears only once.
- **No unwanted elements:** Non-Persian words (e.g. English) and extraneous characters (punctuation is preserved) are removed.
- **Uniform representation:** Morphologically similar words (e.g. different forms of a verb) are converted to a simple base form.
- **Verb simplification:** Conjugated forms are reduced to their base (infinitive) form, with special handling for irregular verbs like "بود" and auxiliary verbs like "هستن".
- **Normalization:** The pipeline corrects spacing issues, replaces thin spaces with regular spaces, and removes zero-width joiners to ensure consistent formatting.

---

## Pipeline Steps

1. **PDF Text Extraction:**  
   - The text is extracted from a PDF file using OCR (with Tesseract) to handle complex Persian encoding issues.
   - The extracted text is normalized with Unicode normalization (NFKC) and reshaped using [arabic-reshaper](https://github.com/mpcabd/arabic-reshaper) and [python-bidi](https://github.com/miurahr/pybidirectional).

2. **Preprocessing:**  
   - English words are removed using regular expressions.
   - Punctuation and numbers are preserved.
   - Special attention is given to normalizing spacing (including replacing thin spaces with normal spaces).

3. **Tokenization & Morphological Segmentation:**  
   - The pipeline uses the [Hazm](https://github.com/sobhe/hazm) and [Parsivar](https://github.com/ICTRC/Parsivar) toolkits to tokenize Persian text and perform morphological analysis, extracting tokens, stems, and lemmas.

4. **Minimal Set Extraction:**  
   - A custom cleaning function filters out redundant tokens, English words, and meaningless fragments.
   - Tokens are standardized by removing extraneous characters and normalizing suffix variations (e.g. ensuring words with and without half‑spaces become identical).

5. **Verb Simplification:**  
   - Conjugated verbs are converted to their simple (base) forms.
   - The pipeline includes specific rules to handle multiple conjugations of common verbs like "بود" and auxiliary verbs like "هستن".
   - If a token contains a separator (e.g. “#” or “&”), only the substring after the separator is retained.

---

## How to Use

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/yourusername/persian-effective-unit-extractor.git
   cd persian-effective-unit-extractor
   ```

2. **Install Dependencies:**

   Make sure you have Python 3 installed. Then, install the required libraries:

   ```bash
   pip install -r requirements.txt
   ```

   *The `requirements.txt` file includes libraries such as `pytesseract`, `pdf2image`, `parsivar`, `arabic-reshaper`, `python-bidi`, and others.*

3. **Run the Pipeline:**

   Adjust the file path in the main script (`main.ipynb` or `main.py`) to point to your Persian text PDF and run the notebook/script:

   ```bash
   jupyter notebook main.ipynb
   ```

4. **Output:**

   The final output is stored as a CSV file containing the minimal set of effective units extracted from the text.

---

## Project Structure

```
├── README.md             # This readme file
├── requirements.txt      # List of dependencies
├── main.ipynb            # Main Jupyter notebook with the full pipeline
├── src/
│   ├── pdf_extraction.py # PDF text extraction and OCR functions
│   ├── preprocessing.py  # Functions to remove English words and normalize spacing
│   ├── morphology.py     # Tokenization and morphological segmentation using Hazm/Parsivar
│   ├── minimal_set.py    # Extraction and cleaning of minimal effective units
│   └── verb_simplification.py  # Verb simplification functions
└── sample.pdf            # Sample Persian text PDF (for testing)
```

---

## Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to check [issues page](https://github.com/yourusername/persian-effective-unit-extractor/issues).

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- [Hazm](https://github.com/sobhe/hazm) for Persian NLP tools.
- [Parsivar](https://github.com/ICTRC/Parsivar) for morphological analysis.
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) and [pdf2image](https://github.com/Belval/pdf2image) for robust PDF text extraction.
- The Persian NLP community for open-source resources and research.

---

*Enjoy extracting effective units from Persian texts!*
