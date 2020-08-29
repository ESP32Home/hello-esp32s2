# hello-esp32s2
sample for esp32s2 environment and simple hello world

* this example is extracted from https://github.com/espressif/esp-idf/tree/master/examples/get-started/hello_world
* the intention is to make idf applications reproducible by defining a clean connection with the IDF environment
* as explained in [espressif updateing release branch](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/versions.html#updating-release-branch), there's nothing else but git commands to swap versions
* installation will use virtual env located in e.g. `$HOME/.espressif/python_env/idf4.1_py3.8_env`
# Environment
Note : as of 29/08/2020 v4.1 only supports esp32s2beta and not esp32s2, so master will be used and this example will be updated to the first release supporting the esp32s2. The master comes with issues commit `6c17e3a64c0` has python depdenecies conflic fixed with update of `esp-idf-master/requirements.txt`
```python
gdbgui==0.13.2.0
pygdbmi==0.9.0.2
```
## First time
* We clone a specific idf branch, then install
```
> git clone --branch tags/v4.1 --recursive https://github.com/espressif/esp-idf.git esp-idf-4.1
> cd esp-idf-4.1
> ./install.sh
```

For prototyping projects using different esp-idf versions, it is more convenient to have the versions in different directories to avoid requiring connection and waisting time on checkouts.
```
|
|- esp-idf-master
|- esp-idf-4.1
|- esp-idf-3.3.2
```

in `.profile`
```
alias get_idf-4.1='. $HOME/esp/esp-idf-4.1/export.sh'
alias idf='idf.py'
alias flash='idf.py -p /dev/ttyUSB0 flash'
alias monitor='idf.py -p /dev/ttyUSB0 monitor'
```
* every call to export will not only export the IDF path (that allows calling .idf.py) but also dependencies such as esptools and xtensa toolchain which versions are linked into the idf version
## Usage
in terminal
```console
> . .profile
> get_idf-4.1
> idf --version
> cd hello-esp32s2
> idf set-target esp32s2
> idf menuconfig
> idf build
> flash && monitor
```

# Hello World Example
Starts a FreeRTOS task to print "Hello World"
