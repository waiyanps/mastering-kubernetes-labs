# Use the official Python base image with tag 3.8-slim
FROM python:3.8-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the application code and requirements file
COPY app.py requirements.txt /app/

# Install the Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port 5000 for the Flask app
EXPOSE 5000

# Set the entrypoint command to run the application
CMD ["python", "app.py"]
