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

To run the code on a vanilla Windows 10 installation, set up your "build" environment first. While most linux distros come with the required software already pre-installed, Windows will need to be setup from scratch.

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
* mingw (`make.exe`)
* perl &nbsp;(`perl.exe`)


<br>

Install `fonttools` as a `fontforge` module:
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
1. Note the location of the `Makefile` and `package.json` files. 

<br>

Update the `Makefile` file so that it uses our freshly-installed `fontforge` module instead:
1. Open the `Makefile` file using you favorite text editor.
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

I would recommend running the commands first on the provided files to test if the environment is working properly. The `Twemoji` working directory should contain a file called `twe-svg.zip` which we can use for our first test.

<br>

[1]
Open a command prompt and navigate to the location of the `Twemoji` working directory.

[2]
To install all dependencies declared in `packages.json`, including `grunt-webfont`, type:

    npm install

[3]
Finally, to build the color-emoji font, type:

    make

[4]
The command builds a color-emoji font from the source SVG files found in the `twe-svg.zip` file, along with any config files saved in the `extras` and `overrides` directories. 

If everything was installed correctly, the output should be saved as `build/Twemoji Mozilla.ttf`.

<br>

## Customizing the output

Once verified that there are no issues running `make`, we can start customizing the font output. Set up a clean slate first:

1. Delete the `build` folder generated earlier.
1. Remove any SVG files in the `overrides` folder.
1. Blank out the `ligatures.json` file inside the `extras` folder. The JSON file should only contain: `[]`.
1. Update all fontnames mentioned inside the `Makefile` and `gruntfile.js` files in the base directory. Avoid using spaces in the fontname. If spaces are required, they need to be escaped with a slash ( `/` ) in the `Makefile` code.

<br>

If custom SVG files will be used, check first if the SVG files are in a compatible format:
* should not contain nested tags
* only include features supported by the COLRv0 spec
* no `url(###)` attributes used for fill or color 

<br>

Most errors occur when the `make` command encounters an SVG file that it cannot processed. If needed, use `picosvg` to simplify complex SVG files to a compatible format. However, this is not a guarantee that the `make` command will process them correctly.

<br>

Observe the following when naming the SVG files: 
* preferably in lowercase, but not required
* file names should use the unicode code point assigned for that particular glyph
* If a glyph requires multiple codepoints, separate each codepoint with dashes ( `-` ) 



<br>
