FROM ubuntu:latest

# Make sure we are up-to-date
# Install the povray binary for Ubuntu
# Create the source directory to be the WORKDIR during execution
# Create the output directory to allow output to go to a different directory
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y autoclean && \
    apt-get -y autoremove && \
    apt-get -y install povray && \
    apt-get -y purge && \
    mkdir /source && \
    mkdir /output

# Set the WORKDIR to /source 
# (the directory containing the .POV source files should be mounted here)
WORKDIR /source

# Set the entrypoint to run povray
ENTRYPOINT ["povray"]