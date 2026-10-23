# KisanMitra - Multilingual Voice Assistant for Farmers, Rural and Elderly Users

One app, one conversation. A farmer can **show a sick leaf** or **just speak** in Hindi or another Indian language.
KisanMitra diagnoses the crop problem, explains the cure, and then keeps helping with crop insurance, loans,
pensions, health information, forms and scam safety - all answered **by voice**.

```
 Leaf photo -> EfficientNet-B0 (train.py) -> diagnosis --+
                                                         v
 Mic -> Groq Whisper -> Groq LLM (+ scheme knowledge base + diagnosis context) -> gTTS voice reply
                              ^
              emergency keyword guard runs first
```
The link between the two halves is the story for judges: after "your tomato has early blight", the farmer can ask
"my crop is badly damaged, can I get money?" and KisanMitra answers using **the diagnosis plus the crop insurance
scheme (report within 72 hours)**.

## Files
| File | Purpose |
|---|---|
| `app.py` | Streamlit UI: big fonts, camera/upload, mic, language and mode selector, autoplay reply |
| `assistant.py` | Prompt, Groq chat call, crop-diagnosis context, emergency detection, text cleanup for speech |
| `vision.py` | Loads the trained model and predicts the disease from a leaf photo |
| `train.py` | Trains the leaf classifier, saves model + metrics + confusion matrix |
| `knowledge.py` | 12 government schemes + scam tips + helplines (**edit and verify this!**) |
| `voice.py` | Groq Whisper speech-to-text and gTTS text-to-speech, 10 languages |

## Setup
```bash
pip install -r requirements.txt
export GROQ_API_KEY=your_key_here        # Windows: set GROQ_API_KEY=your_key_here
```
Optional: `KISANMITRA_LLM` (default `llama-3.3-70b-versatile`) and `KISANMITRA_STT` (default `whisper-large-v3`).
If Groq renames or retires a model, pick another from your Groq console.

## Step 1 - Train the leaf model (free GPU on Colab or Kaggle)
1. Get PlantVillage (Kaggle: "New Plant Diseases Dataset" or "PlantVillage"). Use the folder that directly contains
   one sub-folder per class, e.g. `Tomato___Early_blight/`.
2. `python train.py --data /path/to/PlantVillage`
3. Copy the generated `model/` folder (model.pt, classes.json) next to `app.py`.
   Expect about 97-99% validation accuracy on PlantVillage.

## Step 2 - Run
```bash
streamlit run app.py
```
Open the "Network URL" on your phone (same Wi-Fi) to use the phone camera and mic.
Without `model/`, the leaf-photo section shows a note and the voice assistant still works.

## Before the exhibition
- [ ] **Verify `knowledge.py`** against official sites (pmkisan.gov.in, pmjay.gov.in, pmfby.gov.in...). Amounts and rules change.
- [ ] Test 5-10 real leaf photos (print some), not only dataset images.
- [ ] Test each language you plan to show. Speech recognition is best for Hindi; others vary.
- [ ] Record a backup video (Groq and gTTS need internet).
- [ ] Browsers may block autoplay on first load; tapping the mic once fixes this.
- [ ] Show `model/confusion_matrix.png` and `metrics.json` on a slide.

## Demo script (3 minutes)
1. Language Hindi. Open "Check a crop leaf", upload a tomato blight photo -> diagnosis card + spoken advice.
2. Tap the mic: *"फसल बहुत खराब हो गई, क्या मुझे पैसे मिल सकते हैं?"* -> crop insurance, 72-hour reporting, helpline 14447.
3. Mode "Help with a form": *"मुझे पीएम किसान में नाम लिखवाना है"* -> one question at a time, then documents.
4. Say *"फोन पर कोई OTP मांग रहा है"* -> scam warning and 1930.
5. Say *"सीने में दर्द हो रहा है"* -> red emergency banner (call 108/112) appears instantly, before the AI answer.
6. Switch to Tamil or Punjabi and repeat a question so people see it is truly multilingual.

## Design choices to explain
- **One conversation:** the leaf diagnosis becomes context for every follow-up question.
- **Grounded answers:** scheme facts come from a curated knowledge base; the model is told not to invent amounts.
- **Safety first:** emergency guard runs before the LLM; no OTPs, no medicine or pesticide doses.
- **Accessibility:** voice-first, large fonts, one question at a time, short spoken-style replies with no symbols.

## Honest limitations
- Leaf model is trained on PlantVillage (38 classes, mostly clean lab images); real-field accuracy is lower.
- General information only, not medical, legal or agronomy advice; confirm with KVK / CSC.
- Knowledge base covers 12 central schemes; state schemes vary and are not included.
- Needs internet for speech and the LLM. Voice quality in Gujarati, Kannada, Malayalam can be weaker.

## Ideas if you finish early
- Grad-CAM heatmap showing which part of the leaf the model looked at
- Add your own state's schemes to `knowledge.py`
- Fine-tune on a few real leaf photos you take yourself
- Log questions to a CSV and chart which topics people ask about most
