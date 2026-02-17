# # Use the official Python image as the base image
# FROM python:3.9

# Set the working directory in the container
# WORKDIR /app

# Copy the application files into the container
# COPY . .

# Install necessary packages
# RUN apt-get update && apt-get install -y unixodbc unixodbc-dev
# RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
# RUN curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list
# RUN apt-get update
# RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17

# RUN pip install -r requirements.txt

# Start the FastAPI application
# CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
#CMD uvicorn app:app --host 0.0.0.0 --port 8000
# # Use the official Python image as the base image
# FROM python:3.9

# # Set the working directory in the container
# WORKDIR /app

# # Copy the application files into the container
# COPY . .

# # Install necessary packages
# RUN apt-get update && apt-get install -y unixodbc unixodbc-dev
# RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
# RUN curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list
# RUN apt-get update
# RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17

# RUN pip install -r requirements.txt

# # Start the FastAPI application
# CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
# #CMD uvicorn app:app --host 0.0.0.0 --port 8000
FROM python:3.9

WORKDIR /app

COPY . .

# Install system dependencies (IMPORTANT: curl + gnupg)
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    unixodbc \
    unixodbc-dev \
    ca-certificates

# Add Microsoft signing key (modern way, no apt-key)
RUN curl -sSL https://packages.microsoft.com/keys/microsoft.asc \
    | gpg --dearmor \
    | tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null

# Add Microsoft SQL repo
RUN curl -sSL https://packages.microsoft.com/config/debian/10/prod.list \
    -o /etc/apt/sources.list.d/mssql-release.list

# Install MS ODBC Driver
RUN apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Python deps
RUN pip install --no-cache-dir -r requirements.txt

# Start FastAPI app
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]