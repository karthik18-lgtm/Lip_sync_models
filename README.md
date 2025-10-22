# Lip_sync_models
# Narris AI Lip-Sync Assignment

## Project Overview

This project fulfills the take-home assignment from Narris. The goal was to demonstrate technical skills in exploration, integration, and reuse of open-source technologies by creating a simple web application to perform lip-sync on a static image based on an audio input. The target architecture involved a UI, a model orchestrator, and multiple lip-sync model backends.

## Implemented Models & Final Architecture

After extensive exploration and rigorous testing, it was determined that the primary target models, **Wav2Lip** and **SadTalker**, have **irreconcilable dependency conflicts**. They require fundamentally incompatible versions of core libraries (like PyTorch, NumPy, Pillow, Gradio dependencies, etc.) and cannot be installed within the same environment (e.g., a single Colab notebook).

Therefore, the final working solution implements the target microservice architecture by running each model in its own **separate, isolated environment (separate Colab notebooks)**. This is the standard industry practice for handling such dependency conflicts.

The final system consists of:

1.  Wav2Lip Service (Notebook 1): A dedicated Colab notebook running a Gradio application for Wav2Lip. This represents `Model1 + API1`.
2.  SadTalker Service (Notebook 2)**: A second dedicated Colab notebook running a Gradio application for SadTalker. This represents `Model2 + API2`. This service provides two variations via its UI:
    * SadTalker (Default)**: Full head motion and lip-sync.
    * SadTalker (Still Mode)**: Lip-sync only, no head motion. This serves as the third distinct model option, demonstrating adaptability.

This setup perfectly aligns with the assignment's architecture diagram, treating each notebook as an independent microservice.

## Challenges Encountered

* Irreconcilable Dependency Conflicts**: As detailed above, the core challenge was the inability to co-install Wav2Lip and SadTalker due to conflicting library requirements.
* Inaccessible Models**: A significant number of other potential models explored (Muse Talk, MultiTalk, LatentSync, StyleTalk, DreamTalk, GeneFace++, MakeItTalk, TPSMM) were found to be **no longer publicly accessible**. This was due to private code repositories or dead download links (`404 Not Found`, `401 Unauthorized`) for essential pre-trained model files. This "link rot" is a common real-world problem with older research code.

## Final Solution Rationale

The final solution uses the two robust models confirmed to be functional (Wav2Lip, SadTalker) and runs them in separate environments, accurately reflecting a microservice architecture. The "SadTalker (Still Mode)" variation fulfills the three-model requirement pragmatically, demonstrating adaptability to the technical constraints discovered during exploration.

## Setup and Usage

The project requires running two separate Google Colab notebooks simultaneously.

Prerequisites:
* A Google Account for Google Colab.
* Ensure the Colab runtime is set to use a **GPU** for both notebooks (T4 recommended via Runtime -> Change runtime type).

**Instructions:**

1.  **Notebook 1: Wav2Lip Service**
    * Open `Wav2Lip.ipynb`  in Google Colab.
    * Factory Reset the Runtime: Go to `Runtime` -> `Disconnect and delete runtime`.
    * Run the setup and application cell(s) within the notebook.
    * A public `.gradio.live` URL will be generated. Keep this notebook running.

2.  **Notebook 2: SadTalker Service**
    * Open `SadTalker.ipynb`  in a separate Google Colab session.
    * Factory Reset the Runtime: Go to `Runtime` -> `Disconnect and delete runtime`.
    * Run the setup and application cell(s) within the notebook.
    * A second public `.gradio.live` URL will be generated. Keep this notebook running.

3.  Use the Applications: You can now use the two generated Gradio URLs to interact with each model service independently. During the presentation, you can demonstrate both applications.

## Repository Contents

* `Wav2Lip.ipynb`: The Google Colab notebook containing the setup and Gradio application for the Wav2Lip service.
* `SadTalker.ipynb`: The Google Colab notebook containing the setup and Gradio application for the SadTalker service (including Default and Still modes).
* `README.md`: This file.
