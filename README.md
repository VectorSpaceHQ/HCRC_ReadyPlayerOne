# HCRC_ReadyPlayerOne
A countdown timer used during Hill City Robot Combat competitions.

This repository is for the code used to power the Adruino Mega that controls the LED matrix, et. al., used during the HCRC competitions.

The original code was passed along in a usable state, but was rather untidy and uncommented.

Version 1.2, which is the initial version uploaded to this repository, had two primary objectives:

1) Cleanup and comment the existing code, and
2) Implement several buttons to help control the clock.

## Description of the use case
A HCRC match is a three minute battle between two robot operators. The initial use case was to have a countdown timer that displayed the time remaining in a match with visual indicators of the time remaining in the match.

This use case expanded to include the requirement to have at least four buttons to help control the countdown timer:
1) Two buttons--one for each player--to indicate that the players are ready for the match to begin
2) One button to start the countdown timer
3) One button to reset the clock

The idea is that at the start of the match, the clock will be reset, and the referee will ask each player if they are ready. If the player is ready, they will press their button. Once both buttons have been pressed, the referee can press the button to start the countdown. As time elapses, indicators of the time remaining will be displayed on the LED panel. When the match is finished, the referee will press the reset button to reset the clock.

## Hardware in use
1) Arduino Mega
2) Adafruit 64x32 RGB LED Matrix
3) Arcade style buttons (This may be inaccurate.)

## Libraries used
Adafruit provides two libraries that are used to help drive the LEDs on the panel:

[Adafruit GFX Library](https://github.com/adafruit/Adafruit-GFX-Library)

[RGB Matrix Panel](https://github.com/adafruit/RGB-matrix-Panel)

There is also a library being used that provides extensive timer functionality:

[Count Up Down Timer](https://github.com/AndrewMascolo/CountUpDownTimer)

## General Functionality
Prior to running setup(), the code sets a few definitions and variables. Among these are the Arduino pins that will drive the LEDs. This is used by the libraries to manipulate the LEDs on the panel. The Arduino pins that are connected to the buttons are set at this point, too. (**NOTE:** The variables *must* be changed to the actual pin numbers being used. And it wouldn't hurt to verify the pin assignment for the LEDs, either.) Also, at this point the variables for the length of the match are set as well; currently, it is 3 minutes and 0 seconds.

In setup(), which runs automatically on powering up the Arduino, the hardware is told that the pins assigned to the buttons are to be input, and the function resetClock() is called to reset the clock, so the countdown timer can be used.

Once the clock is reset and ready, the loop() function can start polling the buttons. It first checks to see if the Reset button is pressed.

If it is not it checks to see if the Player One Ready button has been press and if the Player Two Button has been pressed. It will keep checking until both buttons have been pressed.

Once the two player buttons have been pressed, it checks to see if the Start button has been pressed. If it has, it starts the countdown timer.

During the countdown, the LED panel will dispay a signal for the halfway point of the match, a signal for 30 seconds remaining, a five-second warning signal, and a match over signal.

Then it will wait for the Reset button to be pressed.

## Version History
The oldest version in this repository is 1.2. This version is the iteration off of the original from 2018.

### Version 1.2 uploaded November 3, 2019
This is the initially uploaded version. It implements the countdown timer, the LED display, and four buttons.

