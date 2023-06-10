An example of the Docker image building process with a new version (v2.0.0) of the sample Python web application:

**`app.py`**:

```python

import os
from flask import Flask

# Get the port number from the environment variable or use a default value of 5000
port = int(os.environ.get('PORT', 5000))

# Get the default name from the environment variable or use a default value of "Docker"
default_name = os.environ.get('NAME', 'Docker')

# Create a Flask app
app = Flask(__name__)

# Define a route and handler for the root URL
@app.route('/')
def hello():
    return f'Hello, {default_name}! Running on port {port}'

# Start the Flask app on the specified port
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=port)
```
    
    
**`Dockerfile`**:

```bash
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
```

**`Commands`**:

1. Open a terminal or command prompt and navigate to the directory where the Dockerfile and the sample app files are located.

2. Run the following command to build the Docker image:

```bash
docker build -t sample-app:v2.0.0 --build-arg DEFAULT_PORT=5001 --build-arg DEFAULT_NAME="John" .
```

This command builds the Docker image with the tag **`sample-app:v2.0.0`** using the current directory (**`.`**) as the build context. It also passes two build arguments (**`DEFAULT_PORT`** and **`DEFAULT_NAME`**) to set the default values for the corresponding environment variables in the Dockerfile.

3. Once the image is built, you can run a container from it using the following command:

```bash
docker run -d -p 8080:5001 -e PORT=5002 -e NAME="Alice" sample-app:v2.0.0
```
This command starts a container in detached mode (**`-d`**), maps port 8080 on the host to **`port 5001`** inside the container (**`-p 8080:5001`**), and uses the **`sample-app:v2.0.0`** image. It also sets the environment variables **`PORT`** and **`NAME`** to override the default values specified in the Dockerfile.

4. Access the running application by opening a web browser and navigating to http://localhost:8080. You should see the "Hello, Alice! Running on port 5002" message.

In this example, we have added two **`ARG`** instructions in the Dockerfile to specify default values for the port and name. We then use **`ENV`** instructions to set environment variables based on the values provided via the **`ARG`**. The updated **`app.py`** code reads these environment variables to dynamically display the port and name.

Feel free to modify the code or commands according to your specific requirements.
