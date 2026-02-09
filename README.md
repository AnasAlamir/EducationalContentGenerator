# EVA AI Hackathon - Educational Content Generator

This project generates educational training content from a simple catalog using an LLM. For each module, it produces training text, two MCQs, and one flashcard, then packages the results into a ZIP with a manifest for easy submission.

## Highlights
- Cost-aware prompting and batching
- Structured JSON output per module
- ZIP packaging with manifest
- Works with Groq-compatible OpenAI API endpoints

## Repository Structure
```
.
|-- main.ipynb
|-- data/
|   `-- content_catalog.csv
`-- output/
```

## Input
Place your catalog CSV at:
```
data/content_catalog.csv
```

Required columns:
- module_id
- title
- difficulty (Beginner | Intermediate | Advanced)
- duration_min
- format
- tag

Example:
```
module_id,title,difficulty,duration_min,format,tag
M0001,Module 1: Data,beginner,63,quiz,ICAIL
```

## Output
Generated artifacts are written to:
```
output/
  generated_assets.zip
    |-- manifest.json
    `-- generated_content/
        |-- M0001.json
        |-- M0002.json
        `-- ...
```

Each module JSON follows this schema:
```
{
  "module_id": "M0001",
  "generated_text": "...",
  "mcqs": [
    {
      "question": "...",
      "options": ["A", "B", "C", "D"],
      "correct_answer": "A"
    }
  ],
  "flashcards": [
    {
      "front": "...",
      "back": "..."
    }
  ]
}
```

## Quick Start
1. Install dependencies in your environment:
   - openai
   - pandas
   - numpy
   - tqdm
  - python-dotenv

2. Use a local .env file for the API key:
   - Create .env in the project root:
     ```
     GROQ_API_KEY=your_key_here
     ```
   - Ensure .env is gitignored.
   - Restart the terminal or notebook kernel.

3. Open and run [main.ipynb](main.ipynb) top to bottom.

## Notes
- The notebook includes basic rate limiting and retries to handle API limits.
- For large catalogs, increase sleep time or run in smaller batches.