---
resource_id: "7e9270af-fb61-4f46-b80c-d46ad6751503"
---
# Automating Token Counting in Cursor

This guide shows how to automate passing text to the OpenAI tokenizer from within Cursor.

<!-- section_id: "c5df7f24-e956-4756-a5fb-e90a79587bde" -->
## Option 1: Direct Token Counting (Recommended)

Use the `count_tokens.py` script which uses `tiktoken` (OpenAI's official tokenizer) - this gives the same results as the website without needing browser automation.

<!-- section_id: "e6d83f8c-c78f-45de-a915-16aa00ff156c" -->
### Setup:
```bash
pip install tiktoken
```

<!-- section_id: "0c077ea1-8852-4020-8af3-92f96fef2166" -->
### Usage:
```bash
# Count tokens in a file
python count_tokens.py gab.jsonld

# Count tokens with verbose output
python count_tokens.py gab.jsonld --verbose

# Count tokens for specific model
python count_tokens.py gab.jsonld --model gpt-3.5-turbo
```

<!-- section_id: "5db96471-9551-4be2-938a-06edd61936bc" -->
## Option 2: Browser Automation (Clipboard Method)

Use `open_tokenizer.py` to copy text to clipboard and open the tokenizer website.

<!-- section_id: "83d0a420-4934-4f9e-b6fc-4441132baeac" -->
### Setup:
```bash
pip install pyperclip
```

<!-- section_id: "00903e26-ca5c-4808-b675-8225d67d5e69" -->
### Usage:
```bash
# Copy file content to clipboard and open tokenizer
python open_tokenizer.py gab.jsonld

# Or from stdin
echo "Your text here" | python open_tokenizer.py -
```

<!-- section_id: "740aef7a-5894-406e-bfb4-030ddd0ee598" -->
## Option 3: Using Cursor's Browser Automation

You can ask Cursor's AI assistant to:
1. Read a file
2. Navigate to the tokenizer
3. Fill in the text
4. Get the token count

Example prompt:
```
"Read gab.jsonld, navigate to https://platform.openai.com/tokenizer, paste the content, and tell me the token count"
```

<!-- section_id: "63b1c408-5d7f-46be-8e9d-75b42236c1a1" -->
## Option 4: Cursor Command/Shortcut

Create a Cursor command or keyboard shortcut that:
1. Gets the current file or selected text
2. Runs the token counting script
3. Displays the result

You can add this to your Cursor settings or create a custom command.

