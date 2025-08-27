# נשתמש ב־Python רשמי
FROM python:3.10-slim

# נגדיר תיקיית עבודה
WORKDIR /app

# נעתיק את קבצי הפרויקט לתוך הקונטיינר
COPY . /app

# נתקין את התלויות
RUN pip install --no-cache-dir flask

# נחשוף את הפורט שבו Flask ירוץ
EXPOSE 5001

# נריץ את האפליקציה
CMD ["python", "main.py"]
