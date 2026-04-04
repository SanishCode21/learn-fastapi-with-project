# FastAPI - Health Insurance Premium prediction - Streamlit

This is a small end-to-end machine learning project where I built a classification model and exposed it through a FastAPI backend, with a Streamlit frontend.

The application predicts a health insurance premium category (Low/Medium/High) based on user details like age, income, BMI, smoking status, etc.

I built this project mainly to practice building a production-style ML system - not just training a model in a notebook, but actually deploying and connecting it to a frontend.


## 🚀 What This Project Does

### User enters:

- Age
- Height
- Weight
- Annual Income (LPA)
- Smoking status
- City
- Occupation

### Backend:

- Validates input using Pydantic
- Computes BMI
- Applies preprocessing (OneHotEncoding + scaling inside pipeline)
- Runs classification model
- Returns predicted premium category

### Frontend:

- Collects input
- Sends request to FastAPI
- Displays predicted result

## 🛠 Tech Stack
```
    Python 3.12
    FastAPI
    Pydantic v2
    Scikit-Learn (1.8.0)
    Joblib
    Streamlit
    Uvicorn
```

## 📁 Project Structure

```
├── main.py              # FastAPI entry point
├── app.py               # Prediction router
├── model.joblib         # Trained sklearn pipeline
├── frontend.py          # Streamlit UI
├── requirements.txt
├── .gitignore
└── README.md
```

## ⚙️ How to Run This Project

1. Clone the repository
```
git clone <your-repo-url>
cd <project-folder>
```

2. Create virtual environment
```
python -m venv venv
venv\Scripts\activate

(Mac/Linux: source venv/bin/activate)
```

3. Install dependencies
```
pip install -r requirements.txt
```

4. Run FastAPI backend
```
uvicorn main:app --reload
```

Open in browser:

http://127.0.0.1:8000/docs


You can test the /predict endpoint directly from Swagger UI.

5. Run Streamlit frontend
```bash 
streamlit run frontend.py
```
## 🧪 Sample API Request

POST /predict
```
{
  "age": 30,
  "weight": 65,
  "height": 1.7,
  "income_lpa": 10,
  "smoker": false,
  "city": "Mumbai",
  "occupation": "private_job"
}
```

Response:
```
{
  "predicted_category": "High"
}
```

## ⚠️ Issue I Faced (And Fixed)

Initially I got this error while loading the model:

### 1. AttributeError: Can't get attribute '_RemainderColsList'

This happened because:

`Model was trained using scikit-learn 1.6.1 (Google Colab)`
`Backend environment had scikit-learn 1.8.0`

Fix:

`Upgraded sklearn locally to 1.8.0`

`Retrained the model`

`Dumped it again using joblib`
`Loaded the new model in FastAPI`

`After retraining with the same sklearn version, everything worked fine.`

This helped me understand why version consistency is important when deploying ML models.

## 💡 What I Learned

- Building ML pipelines properly
- Keeping preprocessing inside sklearn Pipeline
- Using Pydantic for input validation
- Handling version mismatch errors
- Structuring FastAPI apps with routers
- Connecting backend API with Streamlit frontend
- Debugging serialization issues

## 🔮 Future Improvements

If I extend this further:

- Add Docker support
- Deploy on cloud (Render / AWS / Railway)
- Add probability scores in API response
- Store predictions in database
- Add authentication layer
- CI/CD integration

## 👨‍💻 About Me

Myself Sanish Kumar, I am currently in my 3rd year of the IIT Madras BS Degree in Data Science and Applications.

I am working towards roles in:

`Machine Learning Engineering`
`Backend Development`
`Data Science`

- Name: Sanish Kumar
- Email: sanishbux42@gmail.com
- Linkedin: https://www.linkedin.com/in/sanish-kumar-singh-163679289
- Colab Notebook: https://colab.research.google.com/drive/1rtHc4rRZXT36vVTENj6UqAn3aQas_pgc?usp=sharing
- Acadedmic Github: https://github.com/23f3001252

This project is part of building practical, production-ready ML systems beyond notebooks.

