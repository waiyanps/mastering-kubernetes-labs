# Use the official Python base image with tag 3.8-slim
FROM python:3.8-slim

# Set default values for port and name using ARG
ARG DEFAULT_PORT=5000
ARG DEFAULT_NAME="Docker"

# Set environment variables for port and name using ENV
ENV PORT=$DEFAULT_PORT
ENV NAME=$DEFAULT_NAME

# Set the working directory inside the container
WORKDIR /app

# Copy the application code and requirements file
COPY app.py requirements.txt /app/

# Install the Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port specified by the PORT environment variable
EXPOSE $PORT 

# Set the entrypoint command to run the application
CMD ["python", "app.py"]
