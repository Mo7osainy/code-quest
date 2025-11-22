FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN useradd -s /bin/false -u 1001 voteuser && chown -R voteuser:voteuser /app

USER voteuser

EXPOSE 8080

CMD ["python", "app.py"]
