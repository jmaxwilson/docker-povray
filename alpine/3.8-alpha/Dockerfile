FROM alpine:latest

# This docker image is intended for use with 
# the POV-Ray Extension for Visual Studio Code
# https://github.com/jmaxwilson/vscode-povray
# https://marketplace.visualstudio.com/items?itemName=jmaxwilson.vscode-povray

# Install the required alpine packages
# Clone the POV-Ray code from github
# Make sure we are using the latest stable 3.7 branch of the code
# Prebuild and configuration
# Compile povray from unix source
# Because some branches of the code use a non standard uint instead of unsigned int
#   we use a hack to make sure that it can still compile in alpine linux 
# Cleanup: remove the source code now that povray has been compiled
# Cleanup: remove alpine packages that are no longer needed and add non-dev versions of libraries
# Create the source directory to be the WORKDIR during execution
# Create the output directory to allow output to go to a different directory
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
	sdl-dev \
	ilmbase-dev \
	openexr-dev && \
	git clone https://github.com/POV-Ray/povray.git && \
	cd /povray && \
	git checkout release/v3.8.0 && \
	cd /povray/unix && \
	./prebuild.sh && \
	cd /povray && \
	./configure COMPILED_BY="Docker\n jmaxwilson/povray:3.8-alpha\n https://cloud.docker.com/repository/docker/jmaxwilson/povray" && \
	echo "typedef unsigned int uint;" > uint-hack.h && \
	make CPPFLAGS="-include uint-hack.h -I/usr/include/OpenEXR" && \
	make install && \
	cd / && \
	rm -rf /povray && \
	rm -rf /usr/local/share/doc/povray-3.8 && \
	rm -rf /usr/local/share/povray-3.8/scenes && \
	apk del \
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
	sdl-dev \
	ilmbase-dev \
	openexr-dev && \
	apk add --no-cache \
	boost \
	zlib \
	libpng \
	tiff \
	sdl \
	ilmbase \
	openexr && \
	rm -rf /var/cache/apk* && \
	mkdir /source && \
	mkdir /output

# Set the WORKDIR to /source (the directory containing the .POV source files should be mounted here)
WORKDIR /source

# Set the entrypoint to run povray
ENTRYPOINT ["povray"]
