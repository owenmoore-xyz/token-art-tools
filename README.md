# token-art-tools
Static web application for generative artists to automate random hash seed generation, image capture and features analysis. Developed using React, Gatsby and Semantic UI libraries.

https://owenmoore.github.io/token-art-tools/

![screenshot](docs/preview.jpg)

## Project Configuration

You'll first need to make sure your local development environment is set up to work with this tool.

### Boilerplate Setups

The following boilerplate setups will support Token Art Tools features "out of the box" and are a quick way to get a local web server up and running. I highly recommended trying one or reviewing the setup first.

- **Art Blocks** ~ https://github.com/owenmoore/boilerplate-artblocks-node-setup

### Manual Setup

You must include a provider script in the header of your `index.html` template file. This script enables support for tokenData, screenshots and features capture between your local web server and the hosted web application. Either use this CDN or copy it into your project and link it.

```html
<script src="https://cdn.jsdelivr.net/gh/owenmoore/token-art-tools@main/providers/artblocks.js"></script>
```

#### Canvas is Required

Artwork must be displayed within a `canvas` object in the `body` for all features to work. Many libraries will set this up by default, but if you are unable to get screenshots you may not have a `canvas` set up properly.

#### preserveDrawingBuffer: true

The `preserveDrawingBuffer` must be `true` for screenshots to work.

##### ThreeJS

```javascript
 renderer = new THREE.WebGLRenderer({ preserveDrawingBuffer: true });

```

##### WebGL

```javascript
const gl = canvas.getContext('webgl', { preserveDrawingBuffer: true })
```

#### tokenData in your sketch

The provider script will make a `tokenData` object available for your script to use. It currently contains the hash that is being generated, which you can use to directly access hash pairs or seed RNG functions.

```javascript
var hash = tokenData.hash;
```

### Automation Features

The gear icon in the interface enables two key features: screenshots and feature CSV.


#### Screenshot

Simply set the `number` of hashes to generate and `how long in ms` to wait before attempting an image capture. Err on the side of caution by increasing the wait time if you are getting strange results.

#### CSV Features Report 

In order for Features to be displayed and captured in Token Art Tools, you need to populate the `features` variable (in the provider script) with information. **DO NOT** re-define this variable, simply add information to the object. The application will wait **600ms** before polling, so it's ideal to set this as early as possible.

Example features assignment:

```javascript
features = {
    Palette: "Blue Sky",
    Style: "Shadow",
    Size: 10,
}
```

#### Tips

- Always do a short test of automation first (ex: 10) to see if it's working before commiting to more
- Features capture can sometimes fail or miss generations if the processing is too heavy, try reducing resolution or increasing the wait time betwen generations to minimize dropped information
- Try using the aforementioned *Boilerplate Setups*, they are optimally designed for automation

## Fork & Run App Locally

1. Clone/fork repo
2. `npm install`
3. `make run-server`
4. Open `http://localhost:8000`

## Feature Suggestions & Bugs

Please create an issue in this repository if you have any suggestions or discover bugs.