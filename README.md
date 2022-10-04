# twemoji-colr

Project to create a COLR/CPAL-based color OpenType font from the [Twemoji](https://twitter.github.io/twemoji/) collection of emoji images.

Note that the resulting font will **only** be useful on systems that support layered color TrueType fonts; this includes Windows 8.1 and later, as well as Mozilla Firefox and other Gecko-based applications running on any platform.

Systems that do not support such color fonts will show blank glyphs if they try to use this font.

## Getting started

This project makes use of [grunt-webfont](https://github.com/sapegin/grunt-webfont) and an additional [node.js](https://nodejs.org/en/) script.
Therefore, installation of Node.js (and its package manager [npm](https://www.npmjs.com/)) is a prerequisite. Grunt will be installed as a package dependency — no need to install it globally.

The necessary tools can be installed via npm:

    # install dependencies from packages.json, including `grunt-webfont`.
    npm install

The build process also requires [fontforge](https://fontforge.github.io/) and the TTX script from the [font-tools](https://github.com/behdad/fonttools/) package to be installed, and assumes standard Perl and Python are available.

Both FontForge and font-tools can be installed via `homebrew` on OS X, or package managers on Linux:

    # OS X
    brew install fonttools fontforge

    # Ubuntu, for example
    sudo apt-get install fonttools fontforge python-fontforge

## Building the font

Once the necessary build tools are all in place, simply running

    make

should build the color-emoji font `build/Twemoji Mozilla.ttf` from the source SVG files found in `twe-svg.zip` file and `extras`, `overrides` directories.

<br><br/><hr/><br/>

# Running the code in Windows 10

## Setup the environment

If you plan to run the code on a vanilla Windows 10 installation, we need to do some prep work first.

<br>

Download and install the following:
* Python 3.10.7
* Perl 5.32.1
* Node 16.17.0
* GnuWIn32
* MinGW
* FontForge 2022-03-08

<br>

Afterwards, verify that the locations of the following programs are listed as entries in the system PATH variable: 
* fontforge (`ffpython.exe`)
* python (`python.exe`)
* perl (`perl.exe`)
* mingw (`make.exe`)

<br>

Install `fonttools` as a `font forge` module:
1. Download the `fonttools` repository as a ZIP file from its github page.
1. Extract the contents of the ZIP file to a local directory.
1. Note the location of the `setup.py` file. 
1. On the Start menu, locate and click the `fontforge interactive` entry.
1. Type `cd <local directory>` where `<local directory>` is the folder that contains `setup.py`.  
1. Type `ffpython setup.py install` then press enter to start the installation.
1. After the install process is complete, you can safely close the command prompt window.

<br>

## Update files to run on Windows

Create a working directory:
1. Download this `twemoji` repository as a ZIP file.
1. Extract the contents of the ZIP file to a `<local directory>`.
1. Note the location of the `make` and `package.json` files. 

<br>

Update the `make` file so that it uses our freshly-installed `fontforge` module instead:
1. Open the `make` file using you favorite text editor.
1. Locate the `PYTHON ?= python3` entry.
1. Update this to `PYTHON ?= ffpython`. 
1. Save and close the file.

<br>

Update the `packages.json` to address version conflicts: 
<ol>
<li> Open the <CODE>packages.json</CODE> file using you favorite text editor. </li>
<li> Add the following line as the last JSON entry: <br/><br/>
<pre> 
   "overrides": {
    "graceful-fs": "^4.2.10"
  } </pre><br/></li>
 <li>Save and close the file. </li>
 </ol>
 
 <br>
 
👍 Done!

<br>

## Run the code

Open a command prompt and navigate to the location of the `Twemoji` working directory.

<br>

To install all dependencies declared in `packages.json`, including `grunt-webfont`, type:

    npm install

Finally, to build the color-emoji font, type:

    make

The command builds a color-emoji font from the source SVG files found in the `twe-svg.zip` file, along with any config files saved in the `extras` and `overrides` directories. The output is saved as `build/Twemoji Mozilla.ttf`.

<br>
