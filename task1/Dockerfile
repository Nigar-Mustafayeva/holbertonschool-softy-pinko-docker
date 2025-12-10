cat > Dockerfile <<'EOF'
FROM ubuntu:latest

# Prevent interactive APT prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update and upgrade packages, install Python3 and pip3
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y python3 python3-pip && \
    rm -rf /var/lib/apt/lists/*

# If pip complains about "EXTERNALLY-MANAGED" errors on some systems,
# remove that file before running pip. This is safe inside the container.
RUN rm -f /usr/lib/python*/EXTERNALLY-MANAGED || true

# Install Flask with pip3
RUN pip3 install flask

# Create app directory and copy application code there
WORKDIR /app
COPY ./api.py /app/api.py

# Expose the Flask port
EXPOSE 5252

# Run the Flask app when the container starts
CMD ["python3", "api.py"]
EOF
