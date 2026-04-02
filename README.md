# LLM Product Description Evaluation

This project evaluates the quality of AI-generated product descriptions using a comprehensive rubric and automated LLM-as-a-judge evaluation system.

## Overview

The project consists of two main phases:

1. **Generation Phase**: Generate product descriptions using a language model (Meta-Llama-3.1-8B-Instruct)
2. **Evaluation Phase**: Evaluate the generated descriptions using another language model (Qwen/Qwen3-235B-A22B-Instruct-2507) as an automated judge

## Features

- Automated product description generation from structured product data
- Comprehensive evaluation rubric with 5 quality criteria
- LLM-as-a-judge evaluation system
- Performance metrics tracking (latency, token usage)
- Pass/fail determination based on evaluation scores

## Evaluation Rubric

Each product description is evaluated on 5 criteria:

### 1. Fluency (Natural, easy-to-read sentences)

- **good**: Sentences read naturally with smooth flow and no awkward phrasing
- **ok**: Minor awkward phrasing but overall understandable and readable
- **bad**: Multiple unnatural or difficult-to-follow sentences that disrupt readability

### 2. Grammar (Correct spelling & punctuation)

- **good**: No spelling or punctuation errors
- **ok**: 1 minor grammar/spelling/punctuation error
- **bad**: 2 or more grammar/spelling/punctuation errors

### 3. Tone (Friendly, credible sales voice)

- **good**: Consistently friendly, engaging, and credible sales tone throughout
- **ok**: Mostly appropriate tone with minor inconsistency OR slightly neutral wording
- **bad**: Tone inappropriate, overly formal, robotic, or not aligned with sales voice

### 4. Length (50–90 words)

- **good**: 50–90 words
- **ok**: 40–49 words OR 91–110 words
- **bad**: Less than 40 words OR more than 110 words

### 5. Grounding (Information strictly from provided context)

- **good**: All claims strictly supported by provided information
- **ok**: One minor unsupported detail added
- **bad**: Multiple unsupported claims OR contradicts provided information

## Pass/Fail Criteria

### Pass Rules

A description **passes** if:

- At least 4 criteria are rated "good"
- No more than 1 criterion is rated "bad"

### Automatic Fail Rules

A description **automatically fails** if:

- Grounding is not "good" OR
- Grammar is "bad"

## Requirements

- Python 3.8+
- pandas
- openpyxl
- python-dotenv
- openai (for API client)
- Nebius API access (for LLM calls)

## Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/IsmaelNjama/llm-evaluation.git
   cd llm-evaluation
   ```

2. **Create virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root:

   ```
   NEBIUS_API_KEY=your_nebius_api_key_here
   ```

4. **Prepare input data**
   Place your product dataset Excel file as `Assignment_01_product_dataset.xlsx` with columns:
   - `product_name`
   - `Product_attribute_list`
   - `material`
   - `warranty`

## Usage

1. **Execute cells in order**:
   - Install dependencies
   - Load and prepare data
   - Generate product descriptions
   - Run LLM judge evaluation
   - Parse and view results

2. **View results**
   - Individual evaluation details
   - Performance metrics (latency, token usage)

## Output

The evaluation generates:

- **assignment_01.xlsx**: Complete results with original data, generated descriptions, evaluation scores, and performance metrics
- **Parsed evaluations**: Structured evaluation objects with detailed explanations for each criterion

## File Structure

```
├── evaluation.ipynb              # Main evaluation notebook
├── Assignment_01_product_dataset.xlsx  # Input product data
├── assignment_01.xlsx           # Output results
├── .env                         # Environment variables (API keys)
├── .gitignore                   # Git ignore rules
└── README.md
```

## API Configuration

The project uses Nebius API for LLM calls:

- **Generation Model**: meta-llama/Meta-Llama-3.1-8B-Instruct
- **Judge Model**: Qwen/Qwen3-235B-A22B-Instruct-2507
- **Base URL**: https://api.tokenfactory.nebius.com/v1/

## Customization

You can modify:

- **System prompts** in the notebook for different generation styles
- **Evaluation criteria** by updating the judge prompt
- **Models** by changing the model names in API calls
- **Pass/fail thresholds** in the evaluation logic
