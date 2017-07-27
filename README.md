# Installation Instructions

Clone or download the appropriate SDK repo for Linux from our [GitHub Page](https://github.com/nanoleaf/aurora-sdk-linux)

In the SDK, the `music_processor` python script requires the latest version of the following (non-standard) python packages

* _numpy_
* _pyaudio_
* _librosa_

We highly recommend that you use a virtual environment to install these packages and to run the `music_processor` script. The following instructions will use `virtualenv` to create virtual environments.

Install `virtualenv` with `sudo`:

`sudo pip install virtualenv`

Create and activate a virtual environment called `nanoleaf` (or any other name):

`virtualenv -p python nanoleaf`

`source ./nanoleaf/bin/activate`

Navigate to the top-level SDK directory `aurora-sdk-linux`.

Install numpy:

`pip install numpy`

Install remaining packages:

`pip install -r requirements.txt`

To deactivate the virtual environment:

`deactivate`

# Testing Your Plugin
## Compile Your Plugin
The _AuroraPlugin_ Framework comes with a makefile and a utilities library.
Once you have completed the implementation of your plugin, you can build it using the makefile in the Debug folder. If any additional libraries have been used, the makefile must be modified to link those libraries in as well during linking.

To compile, use a terminal window and change your working directory to the PluginSDK/Debug folder. Use the following commands:

`make clean`

`make`

Once the compilation completes successfully, a **libAuroraPlugin.so** file will be placed in the Debug folder which can be used with the simulator
## Run Your Plugin

Before running the simulator, a symbolic link will have to be made in `/usr/lib` to the libPluginUtilities.so file that is stored in the utilities folder of the AuroraPlugin directory.
To make this link, type the following into terminal.

`ln -s <Path>/Utilities/libPluginUtilties.so /usr/lib/libPluginUtilities.so`

where _Path_ is the absolute path to the Aurora Plugin directory on your computer.

Open up a terminal and change your working directory to the PluginSDK folder. The `music_processor` python script must be run first with a virtual environment, enter:

`source ./nanoleaf/bin/activate`

`python music_processor.py`

Open up another terminal to run the sound module simulator, enter:

`./SoundModuleSimulator -p <absolute path to .so file> -i <ip address>`

If you generated a color palette (see Plugin Builder), enter:

`./SoundModuleSimulator -p <absolute path to .so file> -i <ip address> -cp <absolute path to palette file>`

The *.so* file is the compiled plugin that you wish to run on the Aurora. 

The IP address that you enter is the ip address of the Aurora on the local network. The ip address can be found by using [Bonjour Browser](http://www.tildesoft.com) on Linux.

When using the simulator for the first time, the simulator will attempt to acquire an authentication token from the Aurora and ask the user to hold down the power button on the Aurora for 5-7 seconds. This step is not required during subsequent executions of the simulator. Note: the Simulator will only maintain authentication with one Aurora at a time.

## Plugin Builder
A plugin builder tool can be used to simplify the process of:

* _Pairing with an Aurora_
* _Creating a palette_
* _Building and running plugins_

In the directory plugin-builder-tool/ simply run the command: `python main.py`. A GUI will appear that prompts you to enter the ip address of the testing Aurora, your desired palette, and the absolute path to your plugin in the directory AuroraPluginTemplate/.

Note that the Plugin Builder tool will output information to the terminal. Please check the terminal output for instructions, e.g., during pairing with Aurora or debug printouts from your plugin.
