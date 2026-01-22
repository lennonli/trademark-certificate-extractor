# Trademark Certificate Extractor

A Claude skill for extracting structured information from scanned trademark registration certificates (PDF/image formats) using OCR and LLM-based information extraction.

## Features

- 📄 **Multi-format Support**: Handles PDF, PNG, JPG, JPEG, BMP, TIFF files
- 🌐 **Bilingual OCR**: Tesseract-based text extraction for Chinese and English
- 🤖 **LLM Extraction**: Intelligent information extraction using Claude
- 📊 **Smart Excel Output**: Automatically sorted and grouped by:
  - 注册人 (Registrant) - alphabetical order
  - 有效期限 (Validity Period) - ascending
- 📦 **Batch Processing**: Process multiple trademark certificates at once
- 🖼️ **Logo Extraction**: Automatically extracts and embeds trademark logo images in Excel
- 🎨 **Visual Grouping**: Thick border lines separate different registrant groups

## Extracted Information

- 序号 (Serial Number)
- 商标标识 (Trademark Logo) - embedded as image
- 注册人 (Registrant)
- 注册号 (Registration Number) - from certificate top-right corner
- 国际分类 (International Classification)
- 有效期限 (Validity Period)

## Requirements

### System Dependencies

# macOS
brew install tesseract
brew install tesseract-lang
brew install poppler

# Ubuntu
sudo apt-get install tesseract-ocr
sudo apt-get install tesseract-ocr-chi-sim
sudo apt-get install poppler-utils

### Python Dependencies

pip install openpyxl pdf2image Pillow opencv-python

## Usage

### Quick Start

1. **Extract OCR Text**

python scripts/extract_ocr.py certificate.pdf > extracted_text.txt

2. **Extract Trademark Logo**

python scripts/extract_logo.py certificate.pdf

3. **Extract Information with LLM**

Use the prompt template from `references/llm_prompt.md` with Claude or another LLM to extract structured data.

4. **Generate Excel File**

python scripts/generate_excel.py trademark_data.json

### Batch Processing

# Extract OCR text and logos from all PDFs in a folder
python scripts/batch_extract.py /path/to/certificates

# This will create:
# - *_extracted.txt files for each certificate
# - *_logo.png files for each certificate
# - batch_extraction_results_TIMESTAMP.json with metadata

### Testing

# Test sorting and grouping logic
python scripts/test_sorting.py

# Run complete demo with sample data
python scripts/test_demo.py

## File Structure

```
trademark-certificate-extractor/
├── SKILL.md                           # Skill documentation
├── README.md                          # This file
├── scripts/
│   ├── extract_ocr.py                 # OCR text extraction
│   ├── extract_logo.py                # Trademark logo extraction
│   ├── generate_excel.py              # Excel generation with embedded images
│   ├── batch_extract.py              # Batch processing
│   ├── test_sorting.py              # Sorting logic tests
│   └── test_demo.py                # Complete workflow demo
└── references/
    └── llm_prompt.md               # LLM prompt template
```

## Sorting Rules

The Excel output is automatically sorted and grouped:

1. **Primary Sort**: 注册人 (Registrant) - alphabetically
2. **Secondary Sort**: 有效期限 (Validity Period) - ascending
3. **Visual Grouping**: Thick border lines separate different registrant groups

## Example Output

```
阿里巴巴集团控股有限公司 | 2023-06-01
阿里巴巴集团控股有限公司 | 2025-12-31
阿里巴巴集团控股有限公司 | 2026-03-15
──────────────────────────────────────────────────────────
腾讯科技（深圳）有限公司 | 2024-08-20
腾讯科技（深圳）有限公司 | 2024-12-31
腾讯科技（深圳）有限公司 | 2025-01-10
```

## Installation

1. Download or clone this skill
2. Add it to your Claude skills directory
3. The skill will be automatically available when you need to process trademark certificates

## Troubleshooting

### Tesseract Not Found

```
Error: Tesseract OCR is not installed or not in PATH
```

**Solution**: Install Tesseract OCR and ensure it's in your PATH

### Poor OCR Quality

**Solution**:
- Ensure scans are at 300 DPI or higher
- Try pre-processing images (contrast adjustment, noise reduction)
- Use Tesseract's advanced configuration options

### PDF Processing Fails

**Solution**:
- Install pdf2image: `pip install pdf2image`
- Install Poppler (required by pdf2image)
- macOS: `brew install poppler`
- Ubuntu: `sudo apt-get install poppler-utils`

### Logo Extraction Fails

**Solution**:
- Adjust logo area coordinates in `extract_logo.py` based on certificate layout
- Manually crop and save logo as `<filename>_logo.png`
- Check certificate image quality and resolution

### Missing Fields in Extraction

**Solution**:
- Check OCR quality and completeness
- Try adjusting the LLM prompt
- Manually verify and fill missing fields

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Author

Created with ❤️ for Claude Skills
