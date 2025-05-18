# ใช้ image ที่มี Chrome + Python พร้อมใช้งาน
FROM python:3.10-slim

# ติดตั้ง Chrome และ ChromeDriver
RUN apt-get update && apt-get install -y \
    wget unzip curl gnupg \
    && wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update \
    && apt-get install -y google-chrome-stable \
    && apt-get clean

# ติดตั้ง Python dependencies
WORKDIR /app
COPY . /app
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# เปิดพอร์ต Streamlit
EXPOSE 8501

# คำสั่งเริ่มรันแอป
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
