<a href="https://makc.co">
    <img src="https://makccr.github.io/images/github-header.svg" alt="MAKC lgoo" title="MAKC" align="right" height="60" />
</a>


# Awesome WM Tag Switcher Polybar Module
This is a module for polybar that adds a sort of a tag-list switcher to your polybar.

**Important Note**: In order for this module to function correctly, Awesome WM must be using the standard modkey (Mod4/Left Super), and the default keyboard shortcuts for switching between the tags: Super_L+#1-9. If you don't use the standard key-bindings, you'll have to make some changes to the polybar module to get this working properly.

## Dependencies
* [Awesome WM](https://github.com/awesomeWM/awesome)
* [Polybar](https://github.com/polybar/polybar)
* [``xdotool``](https://github.com/jordansissel/xdotool), is the thing that actually makes this work. I think I can safely assume everyone interested already has Awesome & Polybar installed.

### Additional tools that might be handy
* [Gnome Character Map](https://wiki.gnome.org/action/show/Apps/Gucharmap?action=show&redirect=Gucharmap), ``gucharmap``, for finding custom icons.
* [``xev``](https://www.commandlinux.com/man-page/man1/xev.1.html), if you use alternate keyboard shortcuts and need to do additional configuration.

<p align="center">
<img src="https://raw.githubusercontent.com/makccr/awmp/main/shot.png">
</p>

## Usage
Simply add the following to your polybar modules list, in whatever position and/or order you prefer. Options are ``modules-left =``, ``modules-center =``, or ``modules-right =``. I keep mine in the center.

``1 2 3 4 5 6 7 8 9``

Then at the bottom of your polybar config, paste in the following new modules:
```
[module/1]
type = custom/script
exec = echo "1"
click-left = "xdotool key --clearmodifiers Super_L+1"
[module/2]
type = custom/script
exec = echo "2"
click-left = "xdotool key --clearmodifiers Super_L+2"
[module/3]
type = custom/script
exec = echo "3"
click-left = "xdotool key --clearmodifiers Super_L+3"
[module/4]
type = custom/script
exec = echo "4"
click-left = "xdotool key --clearmodifiers Super_L+4"
[module/5]
type = custom/script
exec = echo "5"
click-left = "xdotool key --clearmodifiers Super_L+5"
[module/6]
type = custom/script
exec = echo "6"
click-left = "xdotool key --clearmodifiers Super_L+6"
[module/7]
type = custom/script
exec = echo "7"
click-left = "xdotool key --clearmodifiers Super_L+7"
[module/8]
type = custom/script
exec = echo "8"
click-left = "xdotool key --clearmodifiers Super_L+8"
[module/9]
type = custom/script
exec = echo "9"
click-left = "xdotool key --clearmodifiers Super_L+9"
```
A sample polybar config with the modules in work can be viewed [here](https://github.com/makccr/dot/blob/bc16321907a06fcfcbec530cea4956945ed90ad2/.config/polybar/config).

### Configuring Icons
By default the module will exist as a line of numbers on your bar that will switch tags on click. In order to customize the icons displayed in the bar, you need to change the output for each of the nine modules. For example, changing ``exec = echo "1"`` to ``exec = echo "•"``, will display a neat, non-numbered row of dots on the bar that have the same functionality; not dissimilar to the sample image provided in this readme.

Additionally, you can use the [``gucharmap``](https://wiki.gnome.org/action/show/Apps/Gucharmap?action=show&redirect=Gucharmap) program to find a more extensive selection of icons to use in tandem with this module.

### Multi-monitor polybar
Something like this works best when your polybar is displayed on all monitors, as the tag switcher will only change tags on the monitor that is active when the icon is pressed. You could build separate polybars for all of your monitors, as many often do, but I have a solution to simply display the same polybar on all connected monitors:

1. In your main polybar config, ``${XDG_CONFIG_HOME}/polybar/config`` / ``~/.config/polybar/config``, add the following under monitor settings:
```
monitor = ${env:MONITOR}
```

2. In your launch script for starting polybar, usually: ``${XDG_CONFIG_HOME}/polybar/launch.sh`` / ``~/.config/polybar/launch.sh``, add the following to the bottom of the script, replacing ``NAMEOFBAR``, with whatever you named your bar, in your polybar config.

```
if type "xrandr"; then
  for m in $(xrandr --query | grep " connected" | cut -d" " -f1); do
    MONITOR=$m polybar --reload NAMEOFBAR &
  done
else
  polybar --reload NAMEOFBAR &
fi
```

An example of both configurations in my personal polybar config, can be found [here](https://github.com/makccr/dot/tree/5407f540280be4bed3bc2a542b541ca6e20f7df4/.config/polybar). If you have any additional questions, I've made a slightly in-depth video about the creation and usage of this module: 

[![Tag Module](https://img.youtube.com/vi/pPoMDfcSdU4/maxresdefault.jpg)](https://youtu.be/pPoMDfcSdU4)


## Development
I am hyper aware that this is, to say the least, a feature-lacking, and sloppy version of what the small group of people wanting a module like this are after. The eventual plan would be to build a proper lua script to more properly enable the desired functionality, and then find a way to integrate it as a proper polybar module. I just haven't found the time to look into doing that yet.  In the mean time, feel free to submit any pull requests that might improve this project in it's current state.
