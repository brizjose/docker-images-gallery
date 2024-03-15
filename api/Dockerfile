# Description: Dockerfile for the API
FROM python:3.9

# Set the working directory in the container
# All files and folders of the application will be copied to this directory
WORKDIR /app

# Port to expose, needs to match the port in the app.py file
EXPOSE 5050

# We first copy the Pipfile and Pipfile.lock to the working directory
# and then install the dependencies
COPY Pipfile Pipfile.lock ./

# Install dependencies
# We use pipenv to manage the dependencies
# The dev-packages are not installed, as they are not needed in the production environment
# These are flagged as [dev-packages] in the Pipfile
RUN pip install --upgrade pip
RUN pip install pipenv
RUN pipenv requirements > requirements.txt
RUN pip install -r requirements.txt

# Copy the application files to the working directory
# For optiimization of the build process, we copy the Pipfile and Pipfile.lock first
# and install the dependencies before copying the rest of the files
# This way, we don't have to reinstall the dependencies every time we change a file
# as Docker caches the layers
COPY . ./

# Run the application
CMD ["python", "main.py"]