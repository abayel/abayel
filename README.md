ai_content_generator/
├── app.py               # Main Python application
├── requirements.txt     # Python dependencies
├── README.md            # Project documentation
├── .gitignore           # Ignore unnecessary files
├── LICENSE              # Project license
├── templates/           # HTML templates
│   └── index.html       # Frontend
└── static/              # Static files (CSS, JS, etc.)
    ├── styles.css       # Styling for the frontend
    └── app.js           # JavaScript for interactivity

from flask import Flask, render_template, request, jsonify
import openai
import os

# Initialize Flask app
app = Flask(__name__)

# Set your OpenAI API key
openai.api_key = os.getenv("OPENAI_API_KEY", "your_openai_api_key")

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/generate", methods=["POST"])
def generate_content():
    data = request.get_json()
    prompt = data.get("prompt", "")

    try:
        response = openai.Completion.create(
            model="text-davinci-003",
            prompt=prompt,
            max_tokens=150,
        )
        content = response.choices[0].text.strip()
        return jsonify({"content": content})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == "__main__":
    app.run(debug=True)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Content Generator</title>
    <link rel="stylesheet" href="/static/styles.css">
</head>
<body>
    <div class="container">
        <h1>AI Content Generator</h1>
        <form id="content-form">
            <label for="prompt">Enter a prompt:</label>
            <input type="text" id="prompt" name="prompt" placeholder="E.g., Write a blog intro about AI" required>
            <button type="button" id="generate-btn">Generate</button>
        </form>
        <div id="result">
            <h2>Generated Content:</h2>
            <p id="generated-content"></p>
        </div>
    </div>
    <script src="/static/app.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    margin: 20px;
    text-align: center;
    background-color: #f4f4f4;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

label {
    font-size: 18px;
    display: block;
    margin-bottom: 10px;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

#result {
    margin-top: 20px;
    text-align: left;
}

#generated-content {
    font-size: 16px;
    background-color: #f9f9f9;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

document.addEventListener("DOMContentLoaded", function () {
    const generateButton = document.getElementById("generate-btn");
    const promptInput = document.getElementById("prompt");
    const generatedContent = document.getElementById("generated-content");

    generateButton.addEventListener("click", async function () {
        const prompt = promptInput.value.trim();
        if (!prompt) {
            alert("Please enter a prompt!");
            return;
        }

        // Send the prompt to the backend
        const response = await fetch("/generate", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ prompt }),
        });

        if (response.ok) {
            const data = await response.json();
            generatedContent.textContent = data.content;
        } else {
            generatedContent.textContent = "Error generating content. Please try again.";
        }
    });
});

Flask
openai

# AI Content Generator

## Overview
This is a Flask-based web application that uses OpenAI's GPT models to generate content based on user prompts.

## Features
- Input text prompts to generate AI-driven content dynamically.
- Simple and user-friendly interface.

## Setup

1. Clone this repository:
    ```bash
    git clone https://github.com/your-username/ai-content-generator.git
    cd ai-content-generator
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Set your OpenAI API key:
    ```bash
    export OPENAI_API_KEY=your_openai_api_key
    ```

4. Run the application:
    ```bash
    python app.py
    ```

5. Open your browser and visit:
    ```
    http://127.0.0.1:5000/
    ```

## License
This project is licensed under the MIT License.

__pycache__/
*.pyc
*.pyo
venv/
.env

MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

git init
git add .
git commit -m "Initial commit"

git remote add origin https://github.com/your-username/ai-content-generator.git
git branch -M main
git push -u origin main

git clone https://github.com/your-username/ai-content-generator.git

