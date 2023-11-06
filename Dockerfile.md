# How to write Dockerfile:
Remeber these '8' basic points to create dockerfile:
--------------------------------------------------------


FROM (Base Image of software e.g, python, ubuntu)

MAINTAINER  (Author of the base image)

ENV (Key-Valy parameter)

COPY/ADD (copy/add files/folders from source to destination)

RUN (To Run the commands and execute the script )

ENTRYPOINT [ "executable" ] (Use any of them only  primary difference is that CMD can be overridden when running the container, while ENTRYPOINT cannot. )
    OR                      
CMD [ "executable" ]            

WORKDIR /the/workdir/path (Set the working directry where you have to execute the commands)

EXPOSE port (Expose the port of Docker container )

=========================================================================================

# Example of Dockerfile

# Use an official Python runtime as the base image
FROM python:3.8

# Set the working directory within the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run the command when the container starts
CMD ["python", "app.py"]

========================================================================================

FROM ubuntu:latest/slim --- Whatever base image you want

WORKDIR /the/workdir/path---- suppose make a folder name with app the you can give "app" folder as path

COPY source dest --- Copy all requirement file from source to destination (. app) 

RUN apt-get update -y && \
     apt-get upgrade -y && \
     Apt-get install -y python3 python3-pip

EXPOSE 80  
ENV NAME World--> ( Here NAME=Key , World=value)

CMD ["python3","app,py"]

====================================================================================

FROM ubuntu

WORKDIR /app

COPY requirements.txt /app
COPY devops /app

RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install -r requirements.txt && \
    cd devops

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]


