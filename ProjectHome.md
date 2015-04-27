# Barcode Writer in Pure JavaScript #

Google Code is closing down.  bwip-js has a new home on github:

> https://github.com/metafloor/bwip-js


All new updates to bwip-js will be provided only on github.  Latest update is v0.11 (April 8, 2015).

Scalable fonts have landed.  The latest versions use an [emscripten](http://kripken.github.io/emscripten-site/) compiled [freetype](http://www.freetype.org/) library to implement scalable fonts.  Versions of OCR-A and OCR-B are embedded in bwip-js plus you can use your own.

## Online Barcode Generator ##

A free [online barcode generator](http://metafloor.github.io/bwip-js/demo/demo.html) is now available.


---


bwip-js is a translation to native JavaScript of the amazing code provided in [Barcode Writer in Pure PostScript](https://github.com/bwipp/postscriptbarcode).  The translated code can run on any browser that natively supports the HTML canvas element or any JavaScript-based server framework that can implement a minimal bitmap graphics interface.

An in-browser demo is provided that mirrors the functionality of the [web-based demo](http://www.terryburton.co.uk/barcodewriter/generator/) provided in BWIPP.

To use the demo, download bwip-js and unpack it.  The download will install to the directory bwip-js.  Then open the file bwip-js/demo.html in your browser and start making barcodes.

The latest versions - along with many older versions - of Google Chrome, Firefox, Opera and Safari work well with the demo.  Internet Explorer 8 and older will not work as they do not implement the canvas element.

Version 0.4 of bwip-js (released 2013-02-26) updates to BWIPP version 2013-01-17 and fixes a bug in the node-js module.

## Barcode Types ##
bwip-js implements the same barcode types as BWIPP.  A comprehensive list includes:

  * AusPost 4 State Customer Code
  * Aztec Code
  * BC412
  * Channel Code
  * Codablock F
  * Code 11
  * Code 128
  * Code 16K
  * Code 25
  * Code 39
  * Code 39 Extended
  * Code 49
  * Code 93
  * Code 93 Extended
  * Code One
  * Data Matrix
  * Deutsche Post Identcode
  * Deutsche Post Leitcode
  * EAN-13
  * EAN-13 Composite
  * EAN-2 (2 digit addon)
  * EAN-5 (5 digit addon)
  * EAN-8
  * EAN-8 Composite
  * Flattermarken
  * GS1 Composite 2D Component
  * GS1 Data Matrix
  * GS1 DataBar Expanded
  * GS1 DataBar Expanded Composite
  * GS1 DataBar Expanded Stacked
  * GS1 DataBar Expanded Stacked Composite
  * GS1 DataBar Limited
  * GS1 DataBar Limited Composite
  * GS1 DataBar Omnidirectional
  * GS1 DataBar Omnidirectional Composite
  * GS1 DataBar Stacked
  * GS1 DataBar Stacked Composite
  * GS1 DataBar Stacked Omnidirectional
  * GS1 DataBar Stacked Omnidirectional Composite
  * GS1 DataBar Truncated
  * GS1 DataBar Truncated Composite
  * GS1-128
  * GS1-128 Composite
  * GS1-14
  * HIBC Codablock F
  * HIBC Code 128
  * HIBC Code 39
  * HIBC Data Matrix
  * HIBC MicroPDF417
  * HIBC PDF417
  * HIBC QR Code
  * ISBN
  * ISMN
  * ISSN
  * ITF-14
  * Interleaved 2 of 5 (ITF)
  * Italian PharmaCode
  * Japan Post 4 State Customer Code
  * MSI Modified Plessey
  * MaxiCode
  * MicroPDF417
  * Miscellaneous symbols
  * PDF417
  * Pharmaceutical Binary Code
  * Pharmazentralnummer (PZN)
  * Plessey UK
  * PosiCode
  * QR Code
  * Rationalized Codabar
  * Raw DAFT succession for custom 4 state symbologies
  * Raw bar space succession for custom symbologies
  * Royal Dutch TPG Post KIX 4-State Barcode
  * Royal Mail 4 State Customer Code (RM4SCC)
  * SSCC-18
  * Telepen
  * Two-track Pharmacode
  * UPC-A
  * UPC-A Composite
  * UPC-E
  * UPC-E Composite
  * United States Postal Service Intelligent Mail
  * United States Postal Service PLANET
  * United States Postal Service POSTNET

## Features ##
bwip-js is almost feature complete.  At present, it lacks the following functionality that exists in BWIPP:
  * Minimal font support.  A public-domain, unencumbered version of the OCR-B typeface has been used to create a series of bitmapped fonts.  These fonts were sized to be compatible with the default 10pt and 12pt font sizes used by BWIPP.
  * Only orthogonal scaling is supported.  This restriction is due to the use of bitmapped fonts.
  * Rotations of 0, 90, 180, and 270 degrees are supported only in the HTML canvas demo.  There are no plans to implement rotation in the PostScript graphics emulation layer.
  * Inkspread is currently hard-coded to 0 in the demo.  Setting it to other values may create non-compliant barcodes.
  * The DataMatrix barcodes do not match the size output by BWIPP (bwip-js barcodes are smaller).  You must use the scale setting to compensate.

bwip-js does _not_ provide a general purpose PostScript emulation layer.  If you came here hoping to find one, you are out of luck.  The PostScript emulation uses a translator that converts all non-graphics code to equivalent JavaScript, and converts all graphics operations to calls into a platform-neutral graphics context.  It is up to the host environment to implement the bitmap interface that is exposed by the graphics context.  An example implementation is provided in the demo.

The PostScript to JavaScript cross-compiler is not included as part of this project; only the translated code is provided.  The cross-compiler is still in its infancy and implements a one-to-one, unoptimized translation of the stack-based PostScript operators.  There is a lot of opportunity to perform peephole optimization and other transforms that convert the code into more efficient JavaScript.

Although the code is not as efficient as it could be, it is still surprisingly fast.  Only with math-intensive symbols (e.g. QRCode with a high level of error correction) is there any appreciable lag.

## Installation ##
Go to [Downloads](http://code.google.com/p/bwip-js/downloads/list) and save the most recent bwip-js package to your computer.

Unzip the download package.  bwip-js will be unpacked into the following directory structure:

```
bwip-js/
	bwip.js			# Main bwip-js module
	demo.html		# The in-browser demo
	node-demo		# An example node-js HTTP server application
	node-bwipjs		# A node-js module that implements bwip-js
	bwipp/			# The cross-compiled BWIPP encoders and renderers
	fonts/			# JavaScript-encoded font files
	lib/			# Utilities required by the demo

```

## Usage ##
bwip-js was designed to run in both client-side and server-side JavaScript environments.  For server-side environments that do not provide a graphics API, there are freely available pure-JavaScript implementations of image file formats like PNG and BMP.  A quick search of the web turns up several possibilities that can be adapted for server-side usage.  See node-bwipjs for an example implementation.

Using bwip-js in your code involves the following steps:
  * Load the main "bwip.js" module.
  * Implement two host-specific interfaces.
  * Create a BWIPJS instance and make a barcode.

Loading "bwip.js" into your JavaScript environment tends to be very platform specific.  If you are working with a CommonJS architecture, then you will likely need to implement a runtime JavaScript loader.  The node-bwipjs file gives an example implementation for node-js:

```
var fs = require('fs');
var vm = require('vm');

function load(path) {
    var text = fs.readFileSync(path);
    if (!text)
        throw new Error(path + ": could not read file");
    vm.runInThisContext(text, path);
}

// Load the primary bwip-js script
load('bwip.js');
```

After bwip.js is loaded and the BWIPJS global is accessible, you must implement two interfaces:
  * Load and execute bwip-js files on demand.  Many of the encoders rely on additional/secondary encoders.  These dependencies are implemented in the PostScript cross-compile as on-demand loading.  Your host implementation must be able to load and execute bwip-js files after the primary encoder has been invoked.  Or you can preload all of the encoders in one shot (that's the strategy the demo takes), but that is a pretty heavy hit every time you generate a barcode.
  * Provide a bitmap graphics interface.  One gotcha here is that you won't know the size of the bitmap until after the encoders have run.  To make it more interesting, you will routinely see negative values for the x,y coordinates.  Therefore, creating a barcode image is always a two step process.  First run the encoder/renderer and record each pixel's coordinates, along with the min/max values for x and y.  Once the encoder has returned, you can determine the bitmap dimensions and render the final image.

Also to keep in mind is that typical graphics environments (HTML canvas, PHP GD, etc.) set their origin (0,0) to the upper left-hand corner.  PostScript uses a page-up orientation and the origin is in the lower left-hand corner.  Since bwip-js implements a direct mapping to the PostScript graphics primitives, the coordinates your bitmap implementation will see have an origin set in the lower left-hand corner.  See the files lib/canvas.js and node-bwipjs for bitmap implementations that convert between the two origin conventions.

Below are the function and object prototypes for the interfaces to implement:

```
// Demand-load encoders, renderers, and fonts.  
// This function is installed as a "class static" method on the bwip-js constructor.
BWIPJS.load = function(path) {
	// path is relative to the bwip-js root directory.  For example, a call to
	// load the one-dimensional barcode renderer will pass the path:
	//		"bwipp/renlinear.js"
	// This implementation must translate the relative path to whatever is
	// required of the server framework and directory structure.
	// bwip-js tracks what has already been loaded (regardless of whether a
	// module was preloaded or demand-loaded).
	// So this interface will only be called when needed.
	...
}

// The bitmap interface.  bwip-js will only call the color() and set() 
// methods during encoding/drawing.  A third method is needed by the 
// host code to render the actual barcode image.
// Note that you can name this object class anything you like.  The
// host code is the only one that references it by name.
function Bitmap() {
	this.color = function(r, g, b) {
		// r,g,b will be integer values between 0 and 255
		// Save as the current color
		...
	};
	this.set = function(x, y) {
		// x,y will be floating point values.  Convert to int.
		x = Math.floor(x);
		y = Math.floor(y);
		
		// Save the coordinates and current color
		...
		// Track the min/max values of x and y
		...
	};
	this.render = function( ... ) {
		// This is your code to render the final bitmap image.
		// Width of the bitmap is:  max_x - min_x + 1
		// Height of the bitmap is: max_y - min_y + 1
		// You will need to offset the pixel coordinates by min_x and min_y.
		// And invert the y-axis if the graphics format you are using has its
		// origin in the upper-left corner.
		...
	};
}
```

Once the host framework is implemented, it's time to invoke an encoder.  You must remember that this is a PostScript emulation, so the calling conventions have a PostScript feel to them.

BWIPP (the PostScript library) uses a two-parameter calling convention.  The first parameter is always the barcode text to be encoded.  The second parameter is the options that govern how the barcode is generated.  This second parameter can be either a string or a PostScript dictionary object.  This author recommends using a dictionary object for the options, as they provide more flexibility when working with options values.

One of the standard options available for linear/one-dimensional barcodes is the alttext option.  This option allows overriding what is printed as the human readable component of the barcode.  If the options are specified as a string, no spaces can occur in the alttext value.  This restriction does not exist if a dictionary object is used.

To invoke a barcode encoder/renderer, you do the following steps:
  * Install the host bitmap interface.
  * Create the dictionary object for the options parameter.
  * Add the necessary options to the object.
  * Push the barcode text onto the PostScript operand stack.
  * Push the options object onto the PostScript operand stack.
  * Invoke the encoder.  bwip-js will automatically demand load the module, if needed.

This next example calls the code128 encoder using the 'parsefnc' option to specify the FNC1 character as part of the barcode text, and provides an alternate, human readable text.

```
// Create a barcode writer instance
var bw = new BWIPJS;

// Create the bitmap interface and pass to the emulator
bw.bitmap(new Bitmap);

// Set the scaling factor
bw.scale(2, 2);

// Create a dictionary object and set the options
var opts = {};
opts.parsefnc    = bw.value(true);
opts.includetext = bw.value(true);
opts.alttext     = bw.value("(00)1234567890");

// Push the barcode text and options onto the operand stack
bw.push("^FNC1001234567890");
bw.push(opts);

// Invoke the encoder and render the barcode
bw.call('code128');
bw.bitmap().render();
```

## Node.js ##
[Node.js](http://nodejs.org) has gained a lot of traction as a server framework but due to its rather unique architecture, integrating bwip-js for use in Node is not a straightforward task.  Included in the bwip-js download (starting with version 0.2) is a fully functional Node module that implements a standard HTTP request handler.  The included example server application demonstrates its usage:

```
var http = require('http');
var bwipjs = require('./node-bwipjs');

http.createServer(function(req, res) {
    // Send all requests to bwip-js.
    // In a real http server, you will want to route requests a bit more
    // intelligently...
    bwipjs(req, res);
}).listen(3030);
```

To use the demo Node server, perform the following steps:
  * Install node.js from the [Download](http://nodejs.org) link.
  * Download and unzip the latest bwip-js [version](http://code.google.com/p/bwip-js/downloads/list).
  * Open a terminal window/command prompt and 'cd' to the bwip-js directory.
  * Run the demo server:
```
  $ node node-demo
```

Once the server is running on your machine, the following link should display a Code 128 bar code in your browser:

http://127.0.0.1:3030/?bcid=code128&text=^FNC1011234567890&scale=4&rotate=L&parsefnc&alttext=(01)01234567890

See the notes in node-bwipjs for details on how to structure the URL for use with the request handler.

The node-bwipjs module provides an example of how to integrate bwip-js into node.js.  It is not production ready.  In particular, the PNG image support is extremely simplistic and will waste a lot of server bandwidth.  256 color depth is used (most bar codes need only two colors) and DEFLATE compression is not implemented.  A native Node implementation of the PNG library with DEFLATE support should greatly reduce image size and CPU utilization.


## Emulator Notes ##
The emulation uses, as much as possible, native JavaScript data types.  Specifically, the following are used by the emulation:
  * Boolean values true and false
  * Null value
  * Numeric values (integer and float)
  * Object (PostScript dictionary object)

You will note that two of the more common JavaScript data types, strings and arrays, are not on the list.  PostScript implements some very powerful semantics with strings and arrays, namely live views into each data type.  For example, you can have a base array plus other references to the array that are offset views into the array elements.  Each view has its own concept of zero-index and length, but these values may or may not match the base array.  Updates to one view causes the base array to be updated and are visible to all other views of the array.

Similar live-view semantics exist for PostScript strings.  Additionally, strings behave more like arrays of character codes rather than JavaScript's usual string semantics.  (PostScript strings actually behave like Uint8 Typed Arrays; if Typed Arrays ever become common place, we can gain some performance by converting the emulation to use it for strings.  The same cannot be said for arrays, since PostScript arrays can store arbitrary data types, similar to JavaScript.)