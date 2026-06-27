# Ai-based-drop-out-prediction-
EduGuard - AI based Student Dropout Prediction System using Machine Learning.  Predicts HIGH/LOW risk students using Logistic Regression &amp; RandomForest.  Shows scholarship and counseling recommendations.


import streamlit as st
import pandas as pd
from sklearn.linear_model import LogisticRegression

st.set_page_config(page_title="EduGuard", page_icon="🎓")
st.title("EduGuard - AI Based Dropout Prediction System")
st.write("Final Year CSE Project 2026")

attendance = st.slider("Attendance Percentage", 0, 100, 75)
marks = st.slider("Average Marks", 0, 100, 60)
fees = st.number_input("Pending Fees Amount", 0, 100000, 0)

if st.button("Predict Dropout Risk"):
    data = {'Attendance': [85, 20, 90, 30], 'Marks': [80, 25, 95, 40], 'Fees': [0, 50000, 5000, 40000], 'Dropout': [0, 1, 0, 1]}
    df = pd.DataFrame(data)
    model = LogisticRegression()
    model.fit(df[['Attendance', 'Marks', 'Fees']], df['Dropout'])
    pred = model.predict([[attendance, marks, fees]])

    if pred[0] == 1:
        st.error("🚨 HIGH RISK: Student may drop out!")
        st.write("Reason: Low attendance/marks or high pending fees")
    else:
        st.success("✅ LOW RISK: Student is safe")
        st.balloons()

st.caption("Final Year CSE Project 2026 | AI Based Dropout Prediction System")
