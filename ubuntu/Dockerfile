FROM ubuntu:latest

# Make sure we are up-to-date
RUN apt-get update
RUN apt-get -y upgrade

#install the povray binary for Ubuntu
RUN apt-get -y install povray

# Create the source directory to be the WORKDIR during execution
RUN mkdir /source

# Create the output directory to allow output to go to a different directory
RUN mkdir /output

# Set the WORKDIR to /source (the directory containing the .POV source files should be mounted here)
WORKDIR /source

# Set the entrypoint to run povray
ENTRYPOINT ["povray"]