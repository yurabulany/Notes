you can further increase mouse speed by decreasing the last number (divisor) of the "Coordinate Transformation Matrix" property. i.e. running `xinput set-prop [device] "Coordinate Transformation Matrix" 1.0, 0, 0, 0, 1.0, 0, 0, 0, 0.3` will increase mouse speed by 1/0.3. editing the libinput conf file located in /etc/X11/xorg.conf.d/ can make this permanent.

'xinput list' command must be used for displaying the list of input devices. id of the device must be used for [device]
