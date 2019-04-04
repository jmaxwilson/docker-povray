# POV-Ray Docker Containers

The [Persistence of Vision Raytracer](http://povray.org) is a high-quality, free software tool for creating three-dimensional graphics by using a Scene Description Language.

You can use these [POV-Ray Docker images](https://hub.docker.com/r/jmaxwilson/povray) to run POV-Ray as a Docker container.

The images have been optimized to be *significantly smaller* than other POV-Ray docker images available.

## POV-Ray Docker Images

|Image:Tags| POV-Ray Version | Size | Base |
|--|--|--|--|
| jmaxwilson/povray | POV-Ray Latest Stable (3.7 Stable) | ≈50MB | alpine |
| jmaxwilson/povray:3.7-stable | POV-Ray 3.7 Stable | ≈50MB | alpine |
| jmaxwilson/povray:3.8-alpha | POV-Ray 3.8 Alpha | ≈37MB | alpine |
| jmaxwilson/povray:ubuntu | POV-Ray Binary from Official Ubuntu/Debian Package | ≈144MB | ubuntu |


## POV-Ray for Visual Studio Code

These dockerized versions of POV-Ray were created for use with the [POV-Ray Extension for Visual Studo Code](https://github.com/jmaxwilson/vscode-povray).


## Usage

    docker run -v [source path]:/source -v [output path]:/output jmaxwilson/povray [scene file] [render options]

### Usage Notes

POV-Ray runs within the container environment. 

Within the container, the working directory is `/source` . So you have to mount the directory containing your source files to the `/source` directory of the container in order for POV-Ray to see them.

Likewise, if you want to render the output to a different path than the source, you need to mount the output path to the `/output` directory of the container. Then in the render options you set the output file name to `/output/`.

### Examples

Run povray to render `scene.pov` in the current directory

    docker run -v $PWD:/source jmaxwilson/povray scene.pov Width=1024 Height=768

Run povray to render `scene.pov` and save the resulting image in a subdirectory called `./images`

    docker run -v $PWD:/source -v $PWD/images:/output jmaxwilson/povray scene.pov Width=1024 Height=768 Output_File_Name=/output/


