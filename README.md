
# Getting started

### Prerequisites:

* Node 8.5.0+ https://nodejs.org/en/
* Python 3.6.1+ https://www.python.org/downloads/
* Install TensorFlow https://www.tensorflow.org/install/

### Steps to run:

```bash
> git clone https://github.com/nanohop/sketch-to-react-native.git
> cd sketch-to-react-native
> npm install && npm link
> sketch-to-react-native ~/Desktop/myfile.svg
```

### Extract the component from Sketch as an SVG:

![Export Instructions](images/export_instructions.png?raw=true)

![Export Instructions 2](images/export_instructions_2.png?raw=true)

### Use that SVG file as the argument for convert.js

```bash
> sketch-to-react-native input-file.svg
```

It will run and save the output to the ./output folder.  Make sure to grab both the .js file, and the associated _images_ folder!  Drop that into your React Native application, and see the magic!

# Conversion process

Sketch exports a fairly clean SVG, which makes the process easier, but there is still a lot of processing involved.  Here's the basic steps:

1. Prep the SVG to make processing easier
2. Use a deep neural net to filter out unwanted elements
3. Get component bounding boxes using headless Chrome
4. Figure out all the child/parent relationships
5. Convert from absolute (pixel) positioning to Flex Box
6. Extract images from SVG paths and polygons
7. Generate styles for every component
8. Generate components
9. Export to an output file


### A note about the most difficult part

Sketch (and the SVG export) is a pixel based (absolute positioned) system - but that's no good for React Native.  One of the primary difficulties was figuring out what the proper parent / sibling relationships were between all the components, and then converting from absolute positioning to flexBox.  There is still some work to clean this part up, but in general it's working fairly well for most inputs.

This also means that components in Sketch can _partially_ overlap - which doesn't do well during the conversion process.  I'm working on a fix for that; but until then - you'll get best results if there are no partially overlapping components in your Sketch file.  (Fully overlapping is fine - those will get properly converted to a parent => child relationship)




