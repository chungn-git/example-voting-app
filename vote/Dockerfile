# Using official python runtime base image
# FROM schoolofdevops/voteapp-python:v0.1.0
FROM python:3.9-slim

# Define variable
ARG PORT
ENV http_proxy=http://web-proxy.corp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.corp.hpecorp.net:8080

# Set the application directory
WORKDIR /app

# Copy our code from the current folder to /app inside the container
COPY . .

RUN python -m pip install --upgrade pip && \
    pip install -r requirements.txt

# Make port 80 available for links and/or publish
EXPOSE 80

# Define our command to be run when launching the container
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
