# Build Stage
FROM python:3.11-slim AS builder

# Install build dependencies for atheris
RUN apt-get update && apt-get install -y \
    clang \
    libclang-dev \
    python3-dev \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install atheris built against Python 3.11
RUN CC=clang CXX=clang++ pip install atheris

FROM python:3.11-slim

# Copy atheris from builder
COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin

ADD . /src
WORKDIR /src
RUN pip install .

CMD ["/src/mayhem/fuzz_url.py"]
