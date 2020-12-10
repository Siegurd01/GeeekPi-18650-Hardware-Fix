# GeeekPi UPS restore on power loss feature fix with 555 timer
Recently I was searching the UPS for RPi 4B and all cheap UPS's (<3$) did not function as an uninterruptible power supply but function as interruptible power supply :) with was sad.
Then I found [GeeekPi 18650](https://aliexpress.ru/item/33011106536.html?spm=a2g0o.productlist.0.0.2c3b4bb5S8H6NC&algo_pvid=a5cdb866-c0a1-4a2b-a3bd-09a6f57ff75d&algo_expid=a5cdb866-c0a1-4a2b-a3bd-09a6f57ff75d-0&btsid=0b8b036316076217905251854ea032&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_&sku_id=67157312088) and it works like a charm:

<p align="center">
  <img width="460" height="300" src="https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/UPS.jpg">
</p>

Except for 1 moment. It does not have a power-on restore function. You must press the button every time the UPS turns off (battery discharge). Therefore, you cannot use this UPS for a stand-alone project.
So I decided make a short fix of this problem. (Of Course I wrote to developers with the please too add this feature (upgrading onboard Nuvoton microcontroller firmware should do the trick) but have no response). 
The solution I found was to add 555 timer with will generate impulses for imitating the button pressing.

Button has 2 function:
 * short pressing - power on
 * long pressing - power off 

The main task was to find the pulse length so that it would turn on the board and, at same time, would not turn it off with periodic repetition.

<p align="center">
  <img width="800" height="600" src="https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/Oscill.jpg">
</p>

Channel 1 is the test impulse and chanel 2 is Vout. So board wake up 830 milliseconds after impulse come.
It turned out that the time of ~70 milliseconds with ~1.2 sec period for the LOW pulse was enough.
So I created scheme of 555 timer with [online calculator](https://ohmslawcalculator.com/555-astable-calculator) (you can use any of them) with the following RC setup:

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/555%20calc.jpg)

## The schematic and wiring:

![](https://github.com/Siegurd01/GeeekPi-18650-Hardware-Fix/blob/main/photo/scheme1.jpg)

You can use own button with fixation on H2 pins for power off the timer and board.
