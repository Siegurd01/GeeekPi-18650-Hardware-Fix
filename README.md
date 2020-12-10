# GeeekPi-18650-Hardware-Fix
GeeekPi UPS restore on power loss feature fix with 555 timer.
Recently I was searching the UPS for RPi 4B and all cheap UPS's (<3$) did not function as an uninterruptible power supply but function as interruptible power supply :) with was sad.
Then I found GeeekPi 18650 and it works like a charm. Except for 1 moment. It does not have a power-on restore function. You must press the button every time the UPS turns off (battery discharge). Therefore, you cannot use this UPS for a stand-alone project.
So I decided make a short fix of this problem. (Of Course I wrote to developers with the please too add this feature (upgrading onboard Nuvoton microcontroller firmware should do the trick) but have no response). 
The solution I found was to add 555 timer with will generate impulses for imitating the button pressing.

Button has 2 function:
 * short pressing - power on
 * long pressing - power off 

The main task was to find the pulse length so that it would turn on the board and, at same time, would not turn it off with periodic repetition.
