FROM python:3.10-slim

# ติดตั้ง Chrome และ ChromeDriver
RUN apt-get update && apt-get install -y \
    wget unzip curl gnupg ca-certificates fonts-liberation \
    libnss3 libatk-bridge2.0-0 libxss1 libasound2 libx11-xcb1 libxcomposite1 libxdamage1 libxrandr2 libgbm1 \
    && wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install -y google-chrome-stable \
    && apt-get clean

# ตั้ง working dir และคัดลอกไฟล์
WORKDIR /app
COPY . /app

# ติดตั้ง Python packages
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# เปิดพอร์ต Streamlit
EXPOSE 8501

# คำสั่งรันแอป
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
