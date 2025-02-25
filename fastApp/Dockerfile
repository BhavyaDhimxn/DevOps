# Use Ubuntu as the base image
FROM ubuntu

# Install Python and dependencies
RUN apt-get update -y
RUN apt-get install -y python3 python3-pip pipenv


# Set the working directory
WORKDIR /app

# Copy the application files
COPY . /app

# Install Python dependencies
RUN pipenv install -r requirements.txt

# Expose the port the app runs on
EXPOSE 8000

# Run the FastAPI server
CMD pipenv run python3 main.py