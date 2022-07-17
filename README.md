# Music-Display-Head-Node
Music Information Source Node

This project is the music source processor that provides the music data to the display nodes via an ad hoc WiFi network.

This system digitizes the music to seven bands of values that range from 0 to 100, plus an average of all seven bands. As is, it reads right and left channels but combines them to one channel of information. It also provides an automatic gain control function using a closed loop algorithm based on an upper and lower threshold of the average number of lights on per audio band.

The values of patter, brightness, squelch, and the softpot are automatically saved in the ESP32 EEPROM and are restored on startup.

The LCD display shows the current AGC level, pattern number, brightness level, softpot, and squelch level.

It uses Infrared Remote control hardware supplied with most every Arduino starter kit.

Here is the system wiring diagram.

![image](https://user-images.githubusercontent.com/11139777/179383187-0bf534e1-a47a-4c30-b947-64a40a318c85.png)

##Hardware
Components used are:
1. ESP32 WROOM, 38 pin version
2. MSGEQ7 Seven Band Spectrum Analyzer Breakout Board
3. 2x16 I2S LCD Display
4. IR Remote Receiver
5. IR Remote Control

It is important to note that the MSGEQ7 board can handle up to the levels a typical computer sound system will output. An attenuator will be necessary for any higher speaker level voltages.

##Software
The software was written using the Arduino IDE and uses these libraries:
1. esp_now
2. WiFi
3. Preferences
4. Taskscheduler
5. LiquirCrystal_I2C
6. IRSmallDecoder

Data packets are sent using the ESP-NOW protocol at around a 50 mS update rate.

The structure of the packet is:
```
struct struct_message
    {
    byte  packetVersion;
    byte  pattern;
    byte  brightness;
    byte  monoAverage;
    byte  softpot;
    byte  channelData[7];
    }
```

##IR Remote Key Commands
- POWER:    Display on/off - stops ALL displays
- PLUS:     Increase LED brightness
- MINUS:    Decrease LED brightness
- NEXT:     Increase pattern number (>>| key)
- PREVIOUS: Decrease pattern number (|<< key)
- MODE:     Display backlight on
- ZERO:     Decrement softpot
- ONE:      Increment softpot
- TWO:      Decrement squelch
- THREE:    Increment squelch

##Debug Output
The ESP USB serial output is set to 115200 bps rate. When connected it responds the following commands:
- 0 - Debug off
- 1 - Output channel packets
- 2 - Show remote control key entries

## Helpful Resources

While not all this information is directly relevant to the operation of the Music Head node, it does apply to understanding the overall system. It is to your benefit to review the following information.

I HIGHLY Recommend you watch this video to learn the difference between LED Strips. There are many different types and each has their strengths and weaknesses. So watch this video first!

[* LED Strips, what's the difference?](https://www.youtube.com/watch?v=QnvircC22hU)

You might want help configuring the Arduino IDE to support the ESP32. Check out this tutorial page from Random Nerd Tutorials.

[* Setting-up Arduino IDE for ESP32](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/)

Once youj've installed ESP32 support in the Arduino IDE, the ESP-NOW and WIFi libraries will be automatically available. Here are some links to helpful technical detail.

[* Technical Overview of ESP-NOW](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/network/esp_now.html#esp-now)

[* Getting Started with ESP-NOW](https://randomnerdtutorials.com/esp-now-esp32-arduino-ide/)

The FastLED library will be a big help to you. Bookmark this site.

[* FastLED Library Home](https://fastled.io/)

   -[* FastLED Color Names](http://fastled.io/docs/3.1/struct_c_r_g_b.html)

Scott Marley has an EXCELLENT YouTube channel filled with tutorials on the FastLED library and some very cool projects. You should take the time to watch these vids from the series, FastLED Basics". Each are shorter than twnety minutes in length.

[* FastLED Basics Part 1](https://www.youtube.com/watch?v=4Ut4UK7612M&t=80s)

[* FastLED Basics Part 2](https://www.youtube.com/watch?v=FQpXStjJ4Vc&t=883s)

[* FastLED Basics Part 3](https://www.youtube.com/watch?v=Ukq0tH2Tnkc)

[* FastLED Basics Part 4](https://www.youtube.com/watch?v=2owTxbrmY-s&t=61s)

[* FastLED Basics Part 5](https://www.youtube.com/watch?v=fRXJQVdwrog&t=292s)

[* FastLED Basics Part 6](https://www.youtube.com/watch?v=7Dhh0IMSI4Q&t=73s)
