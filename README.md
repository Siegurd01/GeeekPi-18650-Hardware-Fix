# GeeekPi UPS restore on power loss feature fix with 555 timer
Recently I was searching the UPS for RPi 4B and all cheap UPS's (<3$) did not function as an uninterruptible power supply but function as interruptible power supply :) with was sad.
Then I found GeeekPi 18650 and it works like a charm:

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/UPS.jpg)

Except for 1 moment. It does not have a power-on restore function. You must press the button every time the UPS turns off (battery discharge). Therefore, you cannot use this UPS for a stand-alone project.
So I decided make a short fix of this problem. (Of Course I wrote to developers with the please too add this feature (upgrading onboard Nuvoton microcontroller firmware should do the trick) but have no response). 
The solution I found was to add 555 timer with will generate impulses for imitating the button pressing.

Button has 2 function:
 * short pressing - power on
 * long pressing - power off 

The main task was to find the pulse length so that it would turn on the board and, at same time, would not turn it off with periodic repetition.

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/Oscill.jpg)

Channel 1 is the test impulse and chanel 2 is Vout. So board wake up 830 milliseconds after impulse come.
It turned out that the time of ~69 milliseconds with ~1 sec period for the LOW pulse was enough.
So I created cheme of 555 timer with [online calculator](https://ohmslawcalculator.com/555-astable-calculator) (you can use any of them) with the folowing RC setup:

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/555%20calc.jpg)

The schematic and wiring:

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/scheme1.jpg)

You can use own button with fixation on H2 pins for power off the timer and board.
