# Ponybar
Simple statusbar generator for dwm.

## Configuration
As usual for the suckless tools, ponybar is configured directly in the source code. The configuration part of `ponybar.c` consists of three sections: configuration defines, function declarations, optimization defines. Overall, you can add or remove functions providing certain measures, and change their formatting.

### Defines
Most of defines are useful, but be careful with MAX ones.

* SEPARATOR - a string to put between different modules
* SLEEP_TIME - status refresh interval
* XXX_FORMAT - format string for corresponding modules
* KBD_LEN - number of symbols to represent current keyboard layout. Use negative value to display full name.
* BAT_* - you need to inspect `/sys/class/power_supply/` directory to correct default values. Current and full file are placed in `BAT_NAME` subdirectory.

### Functions
This part contains function declarations. Use it as a list of available modules for the status bar. Also, add your own functions here. The point of interest is `functab[]` array, where you can put used modules. Each element in the array is defined by the pair of values: first, a name of a function, second, is a number that shows how frequent this function is to call. When the `SLEEP_TIME` define is set to 1, this number is roughly equivalent to the time between calls in seconds.

### Optimization
We don't need unused code, so if not defined USE_MODULENAME the module function is replaced with a dummy function. So if you've added a function to `functab[]` array and got an empty string, add a required define.

## Build
### Manual
* gcc -o ponybar ponybar.c -O2 -s -lX11 -lasound
* mv ponybar /usr/local/bin
* sed -i '/dwm/i \ponybar\&' ~/.xinitrc *(optional step)*

### Make
Use `PREFIX=` to install to the destination other than /usr/local/bin.

* make 
* sudo make install

### Arch Linux
* makepkg
* sudo pacman -U &lt;package_name&gt;

