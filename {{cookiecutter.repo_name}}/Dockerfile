FROM python:3.7-slim as build
RUN apt-get update && apt-get install -y \
    --no-install-recommends \
    build-essential \
    gcc \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/app
RUN python -m venv /usr/app/venv

ENV PATH="/usr/app/venv/bin:$PATH"
COPY requirements.txt .
RUN pip install -r requirements.txt

FROM python:3.7-slim
WORKDIR /usr/app
COPY --from=build /usr/app/venv ./venv
COPY *.py .
COPY *.json .

EXPOSE 8080

ENV PATH="/usr/app/venv/bin:$PATH"
CMD ["python", "main.py"]
