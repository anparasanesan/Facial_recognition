# Face Access Control (Visitor Watch Pro)

A visitor access web app that recognises faces from a webcam photo and keeps a log of every visit. Built with Python, OpenCV, the face_recognition library and Streamlit as an MSc module project.

## Features

- **Add to Database:** enrol a visitor by name with an uploaded photo or a webcam picture. The app stores a 128-number face encoding for them.
- **Visitor Validation:** take a webcam picture. The app finds every face in it, compares each one with the enrolled visitors, and shows the best match above a similarity threshold you choose.
- **View Visitor History:** see every attempt with its time, matched name (or "Unknown") and the saved photo.
- **Clear all data** with one button in the sidebar.

## How it works

1. **Detect:** `face_recognition.face_locations` finds each face in the picture.
2. **Encode:** `face_recognition.face_encodings` turns each face into 128 numbers.
3. **Compare:** the app measures the distance between the new face and every enrolled face, then converts that distance into a 0–1 similarity score.
4. **Decide:** the closest match above the threshold is granted and named. Anything else is logged as "Unknown".
5. **Log:** every attempt is written to the visit history, granted or not.

## Tech stack

Python · OpenCV · dlib / face_recognition · NumPy · pandas · Streamlit · streamlit-option-menu

## Privacy

Face photos and face encodings are biometric data under UK GDPR. This repository contains **no real faces**. The app writes them only to `visitor_database/` and `visitor_history/` on your own machine, and both folders are git-ignored. Clear them with the sidebar button when you finish testing.

## Run it (Windows)

Needs Python 3 and a webcam.

```
python -m venv .venv
.venv\Scripts\activate
pip install cmake
pip install -r requirements.txt
streamlit run app.py
```

The app opens at http://localhost:8501.

**If `dlib` fails to install:** it has to be compiled, which needs the "Desktop development with C++" workload from Visual Studio Build Tools. The other option is a prebuilt dlib wheel that matches your Python version.

**If you want to use a different webcam:** Firefox lets you choose the camera; Chrome may not.

## Limitations

- One photo per person, so recognition depends heavily on lighting and pose.
- No liveness check: a printed photo of an enrolled person could be accepted.
- Encodings are stored in a local CSV file, which suits a demo but not production.

## Credits

- [face_recognition](https://github.com/ageitgey/face_recognition) by Adam Geitgey, built on [dlib](http://dlib.net/).
- The distance-to-confidence formula comes from the face_recognition project wiki.
- [streamlit-option-menu](https://github.com/victoryhb/streamlit-option-menu) for the top menu.

## Author

[Anparasanesan Tharmarajah](https://www.linkedin.com/in/anparasanesan/)
