# 🌾 KisanMitra — A Multilingual AI Assistant for Farmers

**KisanMitra** (meaning *Farmer’s Friend*) is a voice-first AI assistant designed to help farmers, rural families, and elderly users access agricultural guidance and essential information in their preferred Indian language.

The project combines deep learning, generative AI, and speech technologies to make agricultural support more accessible, especially for users who may face language barriers or difficulty navigating text-heavy applications.

## 🎯 Problem Statement

Farmers and rural communities often face challenges such as:
- Identifying crop diseases before they cause significant damage.
- Finding understandable information about government schemes and crop insurance.
- Navigating application procedures and required documentation.
- Accessing digital services that depend on English literacy and typing.

KisanMitra aims to bring these forms of assistance together in one simple, voice-first interface.

## ✨ Key Features

### 🌿 1. AI-Powered Crop Disease Detection
- Accepts a photograph of a crop leaf for analysis.
- Uses an **EfficientNet-B0** deep learning model trained on the PlantVillage dataset.
- Predicts a disease class and provides a confidence score.
- Uses the diagnosis as context for subsequent agricultural questions.

### 🗣️ 2. Multilingual Voice Assistance
- Supports interaction in 10 Indian languages.
- Uses OpenAI Whisper for speech recognition.
- Generates responses using a large language model accessed through Groq.
- Uses Google Text-to-Speech (gTTS) to read answers aloud.

### 🌱 3. Agricultural Guidance
- Provides general information about crop diseases and treatment options.
- Explains recommended next steps in simple language.
- Encourages users to consult local agricultural experts for confirmation.

### 🏛️ 4. Government Scheme Assistance
- Helps users understand schemes such as PM-KISAN and the Pradhan Mantri Fasal Bima Yojana (PMFBY).
- Explains eligibility criteria and commonly required documents.
- Offers step-by-step guidance for navigating application procedures.

### 🛡️ 5. Everyday Information and Safety
- Answers general questions related to health and everyday concerns.
- Helps users recognize potential scams and suspicious claims.
- Aims to make essential information easier to understand through conversational assistance.

## ⚙️ How It Works

1. **User input:** The user uploads a leaf photograph or asks a question using voice.
2. **Image analysis:** The EfficientNet-B0 model predicts the crop disease from the photograph.
3. **Speech recognition:** Whisper converts spoken input into text.
4. **AI response generation:** A Groq-hosted language model generates a contextual response using the available information and crop diagnosis when relevant.
5. **Voice output:** gTTS converts the generated response into speech.
6. **User interaction:** The user can continue the conversation and ask follow-up questions.

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core development |
| PyTorch | Deep learning and model inference |
| EfficientNet-B0 | Crop disease classification |
| PlantVillage | Crop leaf image dataset |
| Groq API | Access to a generative language model |
| OpenAI Whisper | Speech recognition |
| gTTS | Text-to-speech generation |
| Streamlit | User interface and application workflow |

## 🏗️ System Architecture

```text
             User
               |
       Voice or Leaf Image
               |
        Streamlit Interface
               |
       +-------+-------+
       |               |
   Leaf Image       Voice Input
       |               |
 EfficientNet-B0     Whisper
       |               |
 Disease Prediction   Query Text
       |               |
       +-------+-------+
               |
       Contextual AI Response
           (Groq LLM)
               |
       Text / Voice Output
               |
             User
```

## 🎯 Project Objectives

- Make AI-powered agricultural guidance more accessible.
- Reduce language and literacy barriers in digital assistance.
- Combine computer vision with conversational AI in a practical application.
- Explore how voice interfaces can improve technology accessibility for underserved communities.

## ⚠️ Limitations and Responsible Use

- The disease classifier is based on PlantVillage data, so performance on real-world field photographs may differ from performance on dataset images.
- The model covers the crop and disease classes represented in its training data; it cannot identify every possible crop condition.
- AI-generated agricultural recommendations are informational and should be verified with qualified agricultural experts.
- Scheme eligibility, application requirements, and reporting deadlines can change and should be confirmed through official sources.
- Health-related responses are general information, not a substitute for professional medical care.
- Internet access is required for the relevant cloud-based AI and speech services.
- This project is a prototype and has not been presented as a validated, production-ready agricultural advisory service.

## 🚀 Future Scope

- Expand disease detection to additional crops, including rice and wheat.
- Improve robustness using real-world field photographs.
- Add weather forecasts and market-price information.
- Incorporate verified, state-specific government scheme information.
- Explore offline or low-connectivity functionality.
- Improve response reliability through trusted agricultural knowledge sources and expert validation.

## 💡 Learning Outcomes

Building KisanMitra provided an opportunity to explore:
- Deep learning-based image classification.
- Integration of computer vision and generative AI.
- Speech recognition and text-to-speech pipelines.
- Context-aware conversational interactions.
- Designing accessible, multilingual AI applications around real-world problems.

## 👩‍💻 Project Status

**Status:** Prototype / development project

KisanMitra is a project exploring how deep learning, generative AI, and multilingual voice interaction can work together to make agricultural and everyday information more accessible.

---

*Built with the goal of making technology more inclusive, understandable, and useful for the people who need it most.* 🌱
