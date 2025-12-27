# 🤖 AI Ad Generator Agent (n8n + Gemini + Telegram)

An automated AI Agent that turns a simple raw product photo into a professional advertisement in seconds. Built with **n8n**, **Google Gemini**, and **Telegram**.

![Project Banner](https://github.com/i-ayush-7/AI-Ad-Agent-n8n-automation-/blob/main/AD%20AGENT.png)

## 🚀 What It Does
1.  **Input:** User sends a raw product photo (e.g., keyboard, mug, watch) to the Telegram Bot.
2.  **Analysis:** **Google Gemini 2.5 Flash** analyzes the visual features and generates a marketing hook, description, and color palette.
3.  **Creative Generation:** The bot creates a high-quality "Lifestyle" background image using **Pollinations.ai** (Free) or **DALL-E 3**.
4.  **Output:** The bot replies on Telegram with the new professional image and catchy marketing copy.

## 🛠️ Tech Stack
* **Workflow Engine:** [n8n](https://n8n.io/) (Self-hosted)
* **Vision & Copywriting:** Google Gemini 2.5 Flash
* **Image Generation:** Pollinations.ai (Free) or OpenAI DALL-E 3
* **User Interface:** Telegram Bot API
* **Tunneling:** Ngrok

---

## ⚙️ Prerequisites
Before running this project, ensure you have:
* [Node.js](https://nodejs.org/) installed.
* [Ngrok](https://ngrok.com/) installed (for local development).
* A **Google Gemini API Key** (Free from Google AI Studio).
* A **Telegram Bot Token** (From @BotFather).

---

## Prompt

```text
Generate prompt using this {{ $json.message.photo }} image.

And Return ONLY a single JSON object with this exact structure:
{
  "prompt_for_image_generator": You are an expert **Advertisement Prompt Engineer** specializing in computer vision and generative AI. Your goal is to analyze an input image of a product and generate a highly specific, high-fidelity text prompt tailored for **Pollinations AI** to create a professional advertising poster.

**Instructions:**

1.  **Image Recognition (The "Anchor"):**
    * Analyze the provided image deeply.
    * Identify the **Brand** (if visible) and the **Product Type** (e.g., Bike, Car, Cosmetic, Furniture, Watch, Electronic Device, etc.).
    * Identify the key visual attributes that must remain consistent (Color, specific model features, shape, material, texture).

2.  **Constraint - Object Fidelity:**
    * Pollinations AI creates new images from text. To ensure the product looks like the one in the image (without significant changes), your prompt must describe the object *exactly* as it appears in the input image. Do not describe a generic version of the product; describe *this specific* product.

3.  **Prompt Construction for Pollinations AI:**
    * Construct a prompt designed for high-end generative art (Stable Diffusion/Flux style).
    * **Structure:** `[Subject Description] + [Environment/Background] + [Lighting/Mood] + [Style/Quality Keywords]`.
    * **Keywords to Include:** Use terms like "Professional product photography," "Commercial advertisement," "Cinematic lighting," "4k," "Hyper-realistic," "Octane render," "Unreal Engine 5," "Advertising poster."
}
```

## JavaScript Code:

```javascript
// Get the text from Gemini
const rawContent = items[0].json.content || items[0].json.output || "";

// Remove the ```json and ``` markers to leave just the raw JSON
const cleanJson = rawContent.replace(/```json|```/g, '').trim();

// Parse it into a real object
return JSON.parse(cleanJson);
```

## HTTP Request Link:

```url
https://image.pollinations.ai/prompt/{{ $json.prompt_for_image_generator }}
```

## Telegram Message URL:

```url
https://api.telegram.org/bot<YOUR_BOT_TOKEN>/sendMessage?chat_id=<USER_CHAT_ID>&text=Please Subscribe
```

## Project By: Ayush Shukla
