<!-- language -->

[English](README.md) | [简体中文](README_zh-CN.md)

# pdf2markdown

**Author:** textin

**Version:** 1.1.0

**Type:** tool

# Description

[TextIn OCR](https://www.textin.com/register/code/68KPRK) is a general-purpose document parsing service designed specifically for downstream tasks of large language models (LLMs). It can recognize text information from documents or images, including financial reports, national standards, academic papers, corporate announcements, user manuals, financial invoices, and more. It extracts key information and supports restoring the document content into standard Markdown format. TextIn offers OCR text recognition covering more than 10 common document layouts and supports over 52 languages, helping various large models efficiently utilize document data in scenarios such as comprehension, generation, and question answering.

# Setup

1. Get appid & secret code from [Textin User Center](https://www.textin.com/console/dashboard/setting). Refer to the FAQ below for guidance.
2. In the Dify workflow, add the "pdf2markdown" plugin and enter the appid and secret code from Step 1 into the parameter panel.
   ![](./_assets/README_02.PNG)
3. In the "Start" node, add an input item and choose "Single File". You can name the variable as you like, and set the file format to both documents and images, which are supported by TextIn. At the bottom, set the upload method to support both upload and URL.
   ![](./_assets/README_03.PNG)
4. In the document parsing node, type "/" in the input variable field to bring up the variable binding panel, then select file -> url to bind it to the uploaded file from the Start node.
   ![](./_assets/README_04.PNG)
5. Use "Options" to add extra parameters in JSON string format, e.g., {"markdown_details":1, "get_image": "objects"}. For more parameters, refer to the official TextIn API documentation: https://www.textin.com/document/pdf_to_markdown
6. Add a code node to process the returned result. For example, to extract markdown content, bind the entire output of pdf2markdown to the input variable of the "Code" node (e.g., response) and handle it using Python 3, as shown below:
   ![](./_assets/README_06.PNG)

```python
import json

def main(response):
    res = response[0]
    return {
            "markdown": res["result"]["markdown"]
    }
```

# Features

* Highly Accurate Table Recognition: Accurately identifies tables with or without visible borders, as well as dense tables. It handles merged cells and tables spanning multiple pages with ease.
* Ultra-fast Parsing Speed: For documents up to 100 pages, parsing can be completed in as fast as 1.5 seconds. This ensures an exceptional user experience for online applications and significantly reduces offline processing time.
* High Stability: Capable of handling millions of requests per day with a success rate of up to 99.999%. Powered by technology proven in large-scale apps with hundreds of millions of users, ensuring stable and reliable performance.
* Wide Format Support: A single API supports various file formats, including PDF, Word (doc/docx), common image formats (jpg/png/webp/tiff), HTML, Excel(xlsx, csv), PPT(pptx), TXT and more. With one request, you can extract text, tables, heading hierarchy, formulas, handwritten characters, and image information.

# Cases

* Financial Report Data Extraction: Quickly extract and standardize key data from financial documents such as earnings reports and research reports to support data analysis and decision-making.
* Educational Question Bank Cleaning: Efficiently parse various textbooks and exam papers to extract and standardize question data, improving the efficiency of question bank construction.
* RAG Knowledge Base Construction: Analyze unstructured document content and convert it into structured knowledge chunks to empower Retrieval-Augmented Generation (RAG) applications.
* Document Translation with Format Preservation: Combine OCR and document structure analysis to translate multilingual documents while preserving their original formatting.
* Online Grading and Automated Scoring: Recognize and structure student answers to support automated grading and result analysis.
* Online Document Q&A System: Parse documents into a searchable format to support intelligent Q&A systems based on documents, improving information retrieval efficiency.
* RPA/Agent Automation: Serve as a pre-processing module for Robotic Process Automation (RPA) and intelligent agents to enable document recognition, content extraction, and intelligent distribution.

# Q&A

**Q: What types of documents does TextIn support?**
A: It supports a wide range of formats including images (JPG, PNG, etc.), PDF files, Word documents (DOC/DOCX), HTML, Excel(xlsx, csv), PPT(pptx), TXT and more.

**Q: What languages does TextIn support for text recognition?**
A: Currently, it supports over 52 languages, including major ones such as Chinese, English, Japanese, Korean, German, and French.

**Q: What is the output format after document parsing?**
A: The default output is structured Markdown format, and JSON format is also supported for content extraction.

**Q: Are there any usage limits?**
A: Usage limits vary based on the subscription plan and account type, including limits on the number of calls and concurrency. Please refer to the official TextIn OCR documentation for details.

**Q: How do I obtain and manage my API key?**
A: After registering via the [TextIn OCR](https://www.textin.com/register/code/68KPRK), you can generate and manage your APP ID and APP SECRET in the [User Center](https://www.textin.com/console/dashboard/setting) for calling the TextIn OCR service.

**Q: Does TextIn support batch document processing?**
A: Yes, it supports batch uploading of documents via API for recognition and parsing, which is suitable for large-scale document processing.

**Q: Will the parsed document retain the original layout?**
A: TextIn restores the document structure based on common reading order, but extremely complex layouts may undergo some adjustments.

**Q: Are SDKs or code samples provided?**
A: Yes, TextIn offers multi-language SDKs (e.g., Python, Java) and comprehensive API usage examples to facilitate quick integration.
