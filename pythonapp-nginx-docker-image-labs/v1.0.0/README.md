An example of the Docker image building process with a sample Python web application:

1. Create a sample Python web application. Let's assume the following directory structure:

```bash
sample-app/
├── app.py
├── Dockerfile
└── requirements.txt
```
The **`app.py`** file contains a simple Flask web application, and the requirements.txt file lists the Python dependencies.

**`app.py`**:

```python

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello, Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
**`requirements.txt`**:

```
flask
```

2. Create a Dockerfile in the same directory as the sample app:

**`Dockerfile`**:

```bash

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

```

In this Dockerfile, we specify the base image as **`python:3.8-slim`**, set the working directory, copy the app code and requirements file into the container, install the Python dependencies, expose port 5000 for the Flask app, and set the entrypoint command to run the application.

3. Open a terminal or command prompt and navigate to the directory where the Dockerfile and the sample app files are located.

4. Run the following command to build the Docker image:

```bash
docker build -t sample-app:v1.0.0 .
```

This command builds the Docker image with the tag **`sample-app:v1.0.0`** using the current directory (**`.`**) as the build context.

Once the image is built, you can run a container from it using the following command:

```bash
docker run -d -p 8080:5000 sample-app:v1.0.0
```

This command starts a container in detached mode (**`-d`**), maps port 8080 on the host to port 5000 inside the container (**`-p 8080:5000`**), and uses the **`sample-app:v1.0.0`** image.

Access the running application by opening a web browser and navigating to **`http://localhost:8080`**. You should see the **"Hello, Docker!"** message.

That's it! You have successfully built a Docker image for a Python web application, specified the version as v1.0.0, and ran a container from the built image.

Feel free to modify the code or commands according to your specific requirements.
