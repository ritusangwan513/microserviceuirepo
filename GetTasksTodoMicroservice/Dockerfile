# Use the official Python image as the base image
# FROM python:3.9

# # Set the working directory in the container
# WORKDIR /app

# # Copy the application files into the container
# COPY . .

# Install necessary packages
# RUN apt-get update && apt-get install -y unixodbc unixodbc-dev
# RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
# RUN curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list
# RUN apt-get update
# RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17

# RUN pip install -r requirements.txt

# # Start the FastAPI application
# CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
# # Use the official Python image as the base image
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

# Use the official Python image as the base image
# FROM python:3.9

# # Set the working directory in the container
# WORKDIR /app

# # Copy the application files into the container
# COPY . .

# # Install necessary system packages
# RUN apt-get update && \
#     apt-get install -y --no-install-recommends \
#         curl \
#         gnupg \
#         apt-transport-https \
#         lsb-release \
#         unixodbc \
#         unixodbc-dev && \
#     rm -rf /var/lib/apt/lists/*

# # Add Microsoft GPG key and repository using modern method
# RUN mkdir -p /etc/apt/keyrings && \
#     curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/keyrings/microsoft.gpg

# RUN curl https://packages.microsoft.com/config/debian/10/prod.list | \
#     sed 's#deb https://#deb [signed-by=/etc/apt/keyrings/microsoft.gpg] https://#g' \
#     > /etc/apt/sources.list.d/mssql-release.list

# # Install Microsoft ODBC driver
# RUN apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql17

# # Install Python dependencies
# RUN pip install --no-cache-dir -r requirements.txt

# # Start the FastAPI application
# CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
FROM python:3.9

WORKDIR /app

COPY . .

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        gnupg \
        apt-transport-https \
        lsb-release \
        unixodbc \
        unixodbc-dev && \
    rm -rf /var/lib/apt/lists/*

# Add updated Microsoft GPG key
RUN curl -sSL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.gpg

# Add Microsoft repo for Debian Bullseye (works with Python 3.9 base)
RUN echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/microsoft.gpg] https://packages.microsoft.com/debian/11/prod bullseye main" \
    > /etc/apt/sources.list.d/mssql-release.list

# Install Microsoft ODBC driver
RUN apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]