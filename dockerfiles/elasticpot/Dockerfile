FROM python:3.9-alpine

# Install system deps
RUN apk add --no-cache \
    build-base \
    libffi-dev \
    openssl-dev \
    postgresql-dev \
    mariadb-connector-c-dev \
    git \
    linux-headers \
    libpq \
    libxml2-dev \
    libxslt-dev \
    libjpeg-turbo-dev \
    zlib-dev

# Clone the repo
WORKDIR /opt
RUN git clone https://gitlab.com/bontchev/elasticpot.git && \
    cd elasticpot && \
    git checkout d12649730d819bd78ea622361b6c65120173ad45

# Move into cloned repo
WORKDIR /opt/elasticpot

# Install Python requirements
RUN pip install --upgrade pip setuptools && \
    pip install \
        twisted==22.10.0 \
        pyOpenSSL==22.1.0 \
        cryptography==38.0.4 \
        -r requirements.txt

EXPOSE 9200

CMD ["python", "elasticpot.py"]
