# dwmblocks
#### (gm3k4g: this was taken directly from Luke's build)

 NOTE: The original README.md is located below.
==========================

# Building

1. `git clone https://github.com/gm3k4g/dwm`
2. `cd dwm/dwmblocks`
3. `sudo make install`

- This will install `dwmblocks` directly into `/usr/local/bin`.
- Alternatively, if you just want to test and modify `dwmblocks` to your liking without installing, you can simply run `make` instead. Then you can run the generated executable and see if it works as intended.

# Scripts

- There is a `scripts` folder included here. It contains some basic scripts which I edited, and they show things like:
	- Date and time
	- Volume control: Controllable volume with mouse scroll, click to open `pavucontrol`, right click to mute.
	- Internet indicator: Click to open `nm-connection-editor`.
	- Disk usage (storage)
	- Memory usage: Shows memory hoggers.
	- etc.
- If you want more scripts, check the original README below.

To make them work, you'll first want to check these scripts and make sure that you have the required applications installed in order for them to work.

After that's done, you'll want to copy them to your `$HOME/.local/bin` directory, and make them executable. You can do this like so:

1. If it doesn't exist, do `mkdir -p $HOME/.local/bin`, to create the directory.
2. `cp scripts/* $HOME/.local/bin/`, copies all the scripts to the newly created directory.
3. `chmod +x $HOME/.local/bin/*` this will make everything under `$HOME/.local/bin` be executable.

At this point you'll either have to restart your instance of `dwm`, log out and log in again, or just reboot. Afterwards, the scripts should work without any issues.

 Original README.md
==========================

# dwmblocks

Modular status bar for dwm written in c.

# Modifying blocks

The statusbar is made from text output from commandline programs.  Blocks are
added and removed by editing the config.h file.

# Luke's build

I have dwmblocks read my preexisting scripts
[here in my dotfiles repo](https://github.com/LukeSmithxyz/voidrice/tree/master/.local/bin/statusbar).
So if you want my build out of the box, download those and put them in your
`$PATH`. I do this to avoid redundancy in LARBS, both i3 and dwm use the same
statusbar scripts.

# Signaling changes

Most statusbars constantly rerun every script every several seconds to update.
This is an option here, but a superior choice is giving your module a signal
that you can signal to it to update on a relevant event, rather than having it
rerun idly.

For example, the audio module has the update signal 10 by default.  Thus,
running `pkill -RTMIN+10 dwmblocks` will update it.

You can also run `kill -44 $(pidof dwmblocks)` which will have the same effect,
but is faster.  Just add 34 to your typical signal number.

My volume module *never* updates on its own, instead I have this command run
along side my volume shortcuts in dwm to only update it when relevant.

Note that all modules must have different signal numbers.

# Clickable modules

Like i3blocks, this build allows you to build in additional actions into your
scripts in response to click events.  See the above linked scripts for examples
of this using the `$BLOCK_BUTTON` variable.

For this feature to work, you need the appropriate patch in dwm as well. See
[here](https://dwm.suckless.org/patches/statuscmd/).
Credit for those patches goes to Daniel Bylinka (daniel.bylinka@gmail.com).
