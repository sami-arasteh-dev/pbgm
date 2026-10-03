# PBGM — Personal Behavioral Generative Model

**PBGM** is a standalone, browser-based interactive laboratory for modeling human behavior. It integrates a deterministic mathematical engine with Large Language Model (LLM) capabilities to simulate, predict, and reverse-engineer behavioral outcomes based on latent psychological drivers and environmental contexts.

This project is a single-file application (`index.html`) containing all necessary HTML, CSS, and JavaScript. It requires no build steps, no server-side backend, and no external dependencies other than an optional LLM API key for advanced features.

## 📋 Table of Contents
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Technical Details](#technical-details)
- [License](#license)

## ✨ Features

### 1. Hybrid Modeling Engine
*   **Local Mathematical Engine:** Calculates behavioral metrics (e.g., *Control*, *Clarity*, *Intensity*, *Irony*) using weighted linear combinations of latent variables. This runs instantly in the browser without network requests.
*   **AI Integration:** Connects to OpenAI-compatible APIs (default: `api.gapgpt.app`) to provide probabilistic predictions and reverse-engineering of observed behaviors.

### 2. Interactive Visualization
*   **Latent Variable Sliders:** Adjust 16 psychological drivers (e.g., *Attachment*, *Anger*, *Loyalty*, *Uncertainty*) via intuitive sliders.
*   **Real-Time Charts:**
    *   **Bar Chart:** Visualizes the calculated behavioral metrics.
    *   **Timeline:** Shows projected behavioral trends over time.
    *   **Decision Map:** Visualizes the causal flow: `Environment → Internal State → Decision → Behavior → Feedback`.
*   **Draggable Weights:** Click and drag bars on the weight chart to adjust variable values directly.

### 3. Behavioral Metrics (KPIs)
The system calculates and displays key behavioral indicators:
*   **Narrative Control:** The degree to which the subject controls the story.
*   **Transparency:** The clarity and openness of expression.
*   **Expression Intensity:** The emotional strength of the behavior.
*   **Presentation Probability:** The likelihood of performative behavior.

### 4. Reverse Engineering
*   Input an observed behavior (e.g., *"I entered the room calmly but with subtle sarcasm..."*).
*   The AI analyzes the text and infers the likely underlying psychological weights and environmental conditions.
*   These inferred weights can be applied to the model to simulate future behaviors.

## 🏗️ Architecture

The application is built as a **Single Page Application (SPA)** within a single HTML file.

*   **UI Layer:** HTML5 structure with CSS Grid/Flexbox for layout. Supports RTL (Right-to-Left) for Persian/Farsi text.
*   **State Management:** JavaScript objects (`VARS`, `aiState`, `metrics()`) hold the current state of weights, environment, and AI results.
*   **Rendering Engine:** Custom HTML5 Canvas functions (`drawBars`, `drawTimeline`, `drawDecisionMap`) handle all visualizations.
*   **AI Layer:** Asynchronous `fetch` calls to LLM endpoints. Prompts are dynamically generated based on the current state of the model.

## 🚀 Installation

Since PBGM is a client-side application, installation is straightforward:

1.  **Clone or Download:**
    ```bash
    git clone <repository-url>
    # Or simply download the index.html file
    ```
2.  **Open in Browser:**
    Double-click `index.html` to open it in Chrome, Firefox, Safari, or Edge.

**No Node.js, Python, or server setup is required.**

## ⚙️ Configuration

### API Key (Optional)
To use the AI prediction and reverse-engineering features:
1.  Locate the **"Endpoint"** and **"API Key"** fields in the "Language Model" section.
2.  Enter your OpenAI-compatible API key.
    *   *Note:* The key is stored only in the browser's memory for the session. It is not saved to any server.
3.  The default endpoint is `https://api.gapgpt.app/v1/chat/completions`. You can change this to any OpenAI-compatible endpoint (e.g., `https://api.openai.com/v1/chat/completions`).

### Default Parameters
The model initializes with a predefined set of weights and environment settings:
*   **Latent Variables:** 16 variables (e.g., Attachment: 82, Anger: 42, Loyalty: 88).
*   **Environment:** Ambiguity: 82, Identity Threat: 65, Relation: 96, Audience: 75.
*   **Context:** A default Persian text describing a workplace scenario.

## 📖 Usage

### 1. Local Simulation
1.  Adjust the **Latent Variables** sliders to define a psychological state.
2.  Adjust the **Environment** sliders (Ambiguity, Identity Threat, etc.).
3.  Click **"Calculate Behavior"** (محاسبه رفتار).
4.  Observe the updated charts and KPIs.

### 2. AI Prediction
1.  Ensure an API Key is entered.
2.  Click **"AI: Predict Behavior from State"** (AI: پیش‌بینی رفتار از state).
3.  The AI will analyze the current weights and environment and return a JSON response with:
    *   `state_summary`: A textual summary of the internal state.
    *   `behavior_prediction`: A predicted behavioral outcome.
    *   `latent_drivers`: Inferred weights for key drivers.
    *   `confidence`: A confidence score for the prediction.

### 3. Reverse Engineering
1.  Enter an **Observed Behavior** in the text area (e.g., *"I said X, but I felt Y..."*).
2.  Click **"AI: Reverse Engineer from Behavior"** (AI: مهندسی معکوس از رفتار).
3.  The AI will infer the likely weights and environment that produced this behavior.
4.  Click **"Apply AI Weights to Model"** (اعمال وزن‌های AI روی مدل) to update the sliders with the inferred values.

### 4. Copy Prompt
*   Click **"Copy Prompt"** to copy the current system prompt to your clipboard for debugging or external use.

## 🛠️ Technical Details

### Data Flow
1.  **Input:** User adjusts sliders or enters text.
2.  **State Update:** JavaScript updates the `VARS` array and `env()` object.
3.  **Local Calculation:** The `metrics()` function computes behavioral scores using weighted sums.
4.  **Rendering:** Canvas functions redraw charts based on the new metrics.
5.  **AI Interaction (Optional):**
    *   `buildPrompt(mode)` constructs a JSON-structured prompt.
    *   `callAI(mode)` sends the request to the LLM.
    *   `parseJSON(text)` extracts the JSON response.
    *   `applyAI(data)` updates the UI with AI results.

### Key Functions
*   `metrics()`: Calculates behavioral KPIs.
*   `drawBars()`, `drawTimeline()`, `drawDecisionMap()`: Render visualizations.
*   `setupCanvasDrag()`: Enables interactive dragging of chart bars.
*   `buildPrompt()`: Generates context-aware prompts for the LLM.

### Dependencies
*   **None.** All logic is embedded in the HTML file.
*   **External API:** Optional LLM endpoint (OpenAI-compatible).

## 📄 License

This project is provided as-is for educational and experimental purposes. The code is open for modification and use. No warranty is provided.

**Note:** The AI features depend on third-party APIs. Usage of these APIs is subject to the terms of service of the respective providers.
