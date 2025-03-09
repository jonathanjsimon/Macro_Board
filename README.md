# David's Macro Keyboard Build

13-key Ardiono ProMicro USB Macro Keyboard built around retobuiltRyan's MacroKeyboardV2 project. 

Please take a look at Ryan's repository for further information and resources if you are interested in building your own version of this project. 

https://github.com/retrobuiltRyan/MacroKeyboardV2

## Hardware Differences From Ryan's Build

I used the smaller form factory Arduino ProMicro, and used a copy of the board that included USB-C. The Atmega32U4 supports USB 2. The USB-C is only for convenience of the available cables. I saw some comments online referencing some ProMicro USB-C clones using a different pinout than the original ProMicro, so be careful when you purchase.

I used a single rotary encoder on Key 1 rather than multiple encoders. 

I did not include the LED screen. I didn't see the need for it on such a small form factor device.

I added diodes to each key rather than using the diode bypass. This adds some flexibility if I want to use multi-key macros in the future. I used the diodes on Ryan's BOM

I added Mill-Max receptacles to make the keyboard hot-swap. This made the switches sit a bit highter on the board, and added the need of a plate to keep the switches in place, so this change is not for the inexperienced 3D printer. Additionally the receptacles are difficult to solder. The placement and amount of solder must be percise in order to avoid getting solder inside of the receptacle. Getting solder out of the receptacle is extremely difficult, even with a desoldering gun. Ask me how I know.

Mill-Max part number: 3305-0-15-15-47-27-10-0
DigiKey part number: 54-3305-0-15-15-47-27-10-0-ND
DigiKey link: https://www.digikey.com/en/products/detail/mill-max-manufacturing-corp/3305-0-15-15-47-27-10-0/13901972?s=N4IgTCBcDaIKwBYC0BmFAGOT1IIxfyQQHYkxTcccA5AERAF0BfIA

## Code Changes

I used Ryan's Simple Macros file as a jumping off point, but I felt like I made enough changes to his code as to not fork it. Here are the most significant changes that I made: 

Due to the hardware changes, I removed LiquidCrystal_I2C, any references to that library and any reference to the LCD screen =

I used HID-Project rather than the Keyboard and Mouse libraries. HID-Project is much more flexable in what it is capable of. It allows you to send non keyboard/mouse specific HID commands. I am using it here to have the rotary encoder act as a volume knob. I'm sure I'll utalize it much more as I get used to having a macro pad on my desk and come up with some better ideas.

##Planned Updates

###Add an LED Dimmer
Add an LED dimmer multi-key command.
When certain keys are pressed at the same time, put the keypad in a special mode that allows the user to set the brigtness control variable. use the rotary encoder to play with the value, use the keys for presets. exit the mode by pressing the rotary encoder.

###Add Home Assistant support
Add support for Home Assistant so that I can call scenes and automations from the keypad.

###Add Event Support
This is a stretch goal. I'd love to add event support such that when a specific program opens, the macropad receives an event and will change to a specific mode for that program. The easiest way to do this for my setup will be to write a wrapper script that sends an event to the arduino and opens the program for each program I would like to do this with, however I am looking into more generic solutions.