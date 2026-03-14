FROM python:3.11-slim
WORKDIR /app
COPY . .
RUN pip install pytest --break-system-packages
CMD ["python3", "-m", "pytest", "test_app.py", "-v"]