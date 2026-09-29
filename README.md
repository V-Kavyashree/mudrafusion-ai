MudraFusion AI

AI-Powered Bharatanatyam Mudra Recognition and Story Generation System


ABOUT

MudraFusion AI is a Python and Flask-based application that recognizes Bharatanatyam hand gestures from a live camera feed and uses the detected gesture sequence to generate a meaningful story interpretation.

The system combines computer vision, machine learning, semantic similarity, and generative AI to connect hand gestures with relevant verses and generate an accessible story for the user.


FEATURES

• Real-time hand gesture detection using MediaPipe

• Recognition of Bharatanatyam hand gestures using a TensorFlow Lite MLP model

• Normalized hand landmark extraction for model input

• Support for single- and two-hand gesture detection

• Gesture sequence tracking from the live camera feed

• Verse matching using semantic embeddings and keyword similarity

• AI-generated story interpretation using Google Gemini

• Template-based fallback when the AI service is unavailable

• PDF generation of the generated story

• Text-to-speech output

• Flask-based web interface and API routes


HOW IT WORKS

Live Camera
    ↓
MediaPipe Hand Detection
    ↓
Hand Landmark Extraction and Normalization
    ↓
TensorFlow Lite MLP Model
    ↓
Recognized Gesture Sequence
    ↓
Meaning and Synonym Extraction
    ↓
Verse Matching
    ↓
SBERT Semantic Similarity + Jaccard Keyword Similarity
    ↓
Relevant Verse
    ↓
Google Gemini
    ↓
AI-Generated Story
    ↓
PDF / Voice Output


AI AND MACHINE LEARNING PIPELINE

1. HAND LANDMARK DETECTION

MediaPipe Hands detects hand landmarks from the camera stream.

For each detected hand, the system extracts 21 landmarks and normalizes their coordinates relative to the wrist. When only one hand is detected, zero-filled coordinates are used for the second hand so that the model receives a consistent input shape.


2. MUDRA CLASSIFICATION

The normalized landmarks are passed to a TensorFlow Lite Multi-Layer Perceptron (MLP) model.

The model predicts the recognized Bharatanatyam gesture, and predictions are accepted when the confidence exceeds the configured threshold.


3. GESTURE SEQUENCE FORMATION

Detected gestures are tracked over time. A gesture must remain stable for a short duration before being added to the sequence, helping prevent transient predictions from being recorded.


4. VERSE MATCHING

The recognized gesture sequence is converted into a set of symbolic meanings and expanded using predefined synonyms.

The system matches the resulting meanings against stored verses using:

• SBERT (all-MiniLM-L6-v2) for semantic similarity

• Jaccard similarity for keyword overlap

The matching score is used to identify relevant verses.


5. AI STORY GENERATION

The selected verse and detected gesture sequence are passed to Google Gemini.

The application builds a structured prompt containing the gesture sequence, symbolic meanings, verse context, speaker information, translation, and commentary.

Gemini generates a connected explanation of the story represented by the gesture sequence.

A template-based story generator is also available as a fallback when the LLM is unavailable.


TECHNOLOGY STACK

Backend:
Python
Flask
OpenCV

Computer Vision and Machine Learning:
MediaPipe Hands
TensorFlow Lite
NumPy

NLP and AI:
Sentence Transformers
SBERT (all-MiniLM-L6-v2)
Google Gemini

Output:
PDF Generation
Text-to-Speech

Data:
JSON-based gesture meanings
Synonym mappings
Verse data


PROJECT STRUCTURE

app.py - Flask application and camera pipeline

story_engine.py - Verse matching and story generation pipeline

llm_handler.py - Gemini API integration

pdf_handler.py - PDF generation

voice_generator.py - Voice output

generate_csv.py - Data utility

mudra_mlp_model.tflite - Gesture classification model

mudra_meanings.json - Gesture meanings

synonyms.json - Meaning and synonym mappings

b_chapter_1.json - Verse data

templates/ - Flask HTML templates


RUNNING THE PROJECT

1. Clone the repository.

2. Create a Python virtual environment.

3. Activate the virtual environment.

4. Install the required dependencies.

5. Configure the Gemini API key using the GEMINI_API_KEY environment variable.

6. Run the Flask application using:

python app.py

7. Open the application in a browser at:

http://127.0.0.1:5000


APPLICATION FLOW

1. Start the camera.

2. The application detects hand landmarks in real time.

3. The TensorFlow Lite model classifies the detected gesture.

4. Stable gestures are added to the gesture sequence.

5. The sequence is used to identify relevant meanings and verses.

6. The system generates a story interpretation.

7. The result can be viewed and exported through the available output formats.


PURPOSE

MudraFusion AI explores how computer vision and generative AI can be combined to make classical Indian dance gestures more accessible by translating a sequence of hand gestures into an understandable narrative.
