FROM ubuntu:18.04

RUN apt update && \
    apt install -y bash \
    build-essential \
    git \
    curl \
    ca-certificates \
    python3 \
    python3-pip && \
    rm -rf /var/lib/apt/lists

# for drqa for db
ENV LC_ALL=C.UTF-8

RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir \
    torch==1.5.1

RUN mkdir /mfactcheck
WORKDIR /mfactcheck

COPY api/requirements.txt .
RUN python3 -m pip install --no-cache-dir -r requirements.txt

RUN python3 -c "import nltk; nltk.download('punkt')"

COPY app.py .

RUN mkdir -pv src
RUN mkdir -pv scripts
RUN mkdir -pv static
RUN mkdir -pv templates

COPY src src
COPY static static
COPY templates templates

ENV PYTHONPATH "${PYTHONPATH}:src"
ENV FLASK_APP app:app

CMD ["flask run", "--host=0.0.0.0", "--port=8080", "--call", "app:app"]