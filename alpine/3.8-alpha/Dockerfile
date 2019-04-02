FROM alpine:latest

# This docker image is intended for use with 
# the POV-Ray Extension for Visual Studio Code
# https://github.com/jmaxwilson/vscode-povray
# https://marketplace.visualstudio.com/items?itemName=jmaxwilson.vscode-povray

# Install the required alpine packages
RUN apk add --update --no-cache \
	git \
	coreutils \
	build-base \
	autoconf \
	automake \
	bash \
	boost-dev \
	zlib-dev \
	libpng-dev \
	tiff-dev \
	sdl-dev

# Clone the POV-Ray code from github
RUN git clone https://github.com/POV-Ray/povray.git

WORKDIR /povray

# Make sure we are using the latest stable 3.8.0 branch of the code
RUN git checkout release/v3.8.0

# Prebuild and configuration
RUN cd unix && ./prebuild.sh
RUN ./configure COMPILED_BY="Docker\n jmaxwilson/povray:3.8-alpha\n https://cloud.docker.com/repository/docker/jmaxwilson/povray"

# Compile povray from unix source
# Becase the some branches of the code uses a non standard uint instead of unsigned int
# we use a hack to make sure that it can still compile in alpine linux 
RUN echo "typedef unsigned int uint;" > uint-hack.h
RUN make CPPFLAGS="-include uint-hack.h"
RUN make install

WORKDIR /

# Cleanup: remove the source code now that povray has been compiled
RUN rm -rf /povray

# Cleanup: remove alpine packages that are no longer needed
RUN apk del build-base autoconf automake gcc libstdc++ git perl python3 python2
RUN rm -rf /var/cache/apk*

# Create the source directory to be the WORKDIR during execution
RUN mkdir /source

# Create the output directory to allow output to go to a different directory
RUN mkdir /output

# Set the WORKDIR to /source (the directory containing the .POV source files should be mounted here)
WORKDIR /source

# Set the entrypoint to run povray
ENTRYPOINT ["povray"]
