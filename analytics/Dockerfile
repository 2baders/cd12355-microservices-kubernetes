# Use a Python base image
FROM public.ecr.aws/docker/library/python:3.10-slim

# Set the working directory
WORKDIR /app

# Copy the requirements file
COPY requirements.txt .

# Install dependencies
RUN pip install -r requirements.txt && pip install werkzeug==2.2.2

# Copy the rest of the app
COPY . .

# Run the app
CMD ["python", "app.py"]
