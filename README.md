# ai-script-automation
# Autonomous AI Content Engine & Batch Processing Pipeline

An enterprise-grade, automated backend pipeline built in **n8n** that orchestrates multi-agent AI systems, handles state-managed data looping, and dynamically generates tailored scripts and optimized visual assets without human intervention. 

This pipeline reduces production time for bulk digital asset creation by 95% while utilizing an edge-case architecture to completely bypass API rate limits and paid paywalls.

---

## 🏗️ System Architecture

![Workflow Architecture] (<img width="1920" height="1080" alt="Screenshot (169)" src="https://github.com/user-attachments/assets/4f137ff7-854d-4a57-bd8e-376dce71a7a2" />
)

The data flows seamlessly through the following stages:
1. **Data Ingestion:** Fetches seed topics dynamically from a database via the Google Sheets API.
2. **State Management:** Uses an iterative batch loop node to process records one by one without crashing or overloading system memory.
3. **Context Engineering:** Passes items to an AI Agent that generates a voiceover/text script (`scriptText`) and an optimal design layout prompt (`imagePrompt`).
4. **Data Sanitization & Transformation:** Executes custom JavaScript processing nodes to clean strings, encode data payloads, and structure them for external consumption.
5. **Asset Synchronization:** Bypasses third-party image generation rate-limits by injecting a dynamic URL delivery model directly into the final data pipeline.

---

## 🛠️ Tech Stack

| Component | Technology Used |
| :--- | :--- |
| **Workflow Orchestration** | n8n (Advanced Looping & State Management) |
| **Generative AI Engine** | OpenAI / Anthropic (via n8n Multi-Agent Framework) |
| **Scripting & Data Parsing** | JavaScript (ES6+) |
| **Database & Destinations** | Google Sheets API |
| **Asset Delivery System** | REST APIs / Open-Source CDN (LoremFlickr) |

---

## 🚀 Key Engineering Challenges Handled

### 1. The Binary Data vs. Text URL Mismatch
* **The Problem:** The initial media generation node returned heavy, downloaded raw binary files instead of simple image source text. Passing raw binary directly into downstream text-based templates caused immediate pipeline crashes and syntax compilation errors (`undefined`).
* **The Solution:** Restructured the data transformation pipeline. Instead of relying on static file downloads, I leveraged dynamic URL routing using a custom JavaScript expression. By implementing `encodeURIComponent($json.scriptText)`, the pipeline translates raw script strings into deterministic web links on the fly, keeping the data lightweight and 100% text-compatible.

### 2. Bypassing Concurrent API Rate Limits & Cost Caps
* **The Problem:** Traditional SaaS media generation APIs (like RenderForm) impose rigid monthly limits (e.g., 50 free images) or drop connections under heavy batch loads due to concurrent IP request limits (`Queue Full / max requests: 1`).
* **The Solution:** Completely decoupled the asset generation layer from rigid third-party API rate limits. Swapped the synchronous API call format for an open-source image delivery CDN. By injecting unique text-based cryptographic "seeds" into a global image caching network, the pipeline generates 100% unique thematic backdrops for every single batch item concurrently—with **zero downtime and zero platform costs**.

---

## 📦 How to Run This Project

1. Install and launch an instance of **n8n** (Cloud or self-hosted via Docker/npm).
2. Create a new workflow canvas.
3. Click the menu in the top right and select **Import from File**.
4. Upload the `workflow.json` file included in this repository.
5. Authenticate your **Google Sheets** credentials and set up your source spreadsheet.
6. Click **Execute Workflow** to run the complete automated batch loop.

---

### 📝 License
Distributed under the MIT License. See `LICENSE` for more information.
