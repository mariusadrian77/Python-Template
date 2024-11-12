FROM python:3.11.3-slim-bullseye

ENV POETRY_NO_INTERACTION=1 \
    POETRY_VIRTUALENVS_CREATE=false \
    POETRY_HOME=/usr/local \
    POETRY_CACHE_DIR=/tmp/poetry_cache \
    WORKING_DIR=/code/

# Install system dependencies
RUN apt-get update && \
    apt-get install -y \
    git \
    curl \
    build-essential \
    libpq-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python -

# Install pip and upgrade it
RUN pip install --no-cache-dir --upgrade pip

WORKDIR $WORKING_DIR

# Copy only pyproject.toml first
COPY pyproject.toml ./

# First install main dependencies
RUN poetry install --no-root --only main

# Copy the rest of the application
COPY . .
