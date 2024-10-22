**This repository contains the KiCad project, gerber, BOM and other associated files for MicroPro RP2040, a custom RP2040 based dev board compatible with Sparkfun ProMicro RP2040.**

![[Cover]](.pic/cover-1200px.jpg)

The RP2040 is a great microcontroller, plenty powerful, well documented, and cheap. However, its on board ADC kinda sucked. I have another project which incorporates a Sparkfun ProMicro RP2040 board that uses the ADC, and I wish I can get more out of it. 

I really liked the ProMicro form factor. It's relatively small, has plenty of flash and enough GPIO. I also thought it might provide an upgrade path, which turned out to be correct(though that's long before RP2350 was announced). So I decided to design a custom board with a better stand-alone ADC that's drop-in compatible. Meaning the pinout has to stay the same, and the input to the ADC has to be muxed.

The analog pins of the RP2040 (GP26-GP29) are directly wired to the board's pads. While those four pads are also connected to *tmux1204*, a 4:1 mux, whose drain is connected to the *ads7042*, a 1-MSPS, 12-bit, single channel ADC.

![[mux-adc]](.pic/mux-adc.png)

By default, this board should behave no differently than the original. To use the stand-alone ADC, you need to first configure the multiplexer to connect the right pin to the ADC and set the corresponding RP2040 pin to input. This provides better ADC performance, and in theory can achieve 1M sampling rate, double what the on board ADC can do. (Not tested yet.) Though the input filter may need to be redesigned for such high sampling rate.

**Differences**
Though this board is designed to be compatible with Sparkfun ProMicro RP2040, there are a number of differences. First, most significantly, this is a double sided board. Therefore by default it does not have castellated pads, thought a castellated footprint is provided. Second, the push buttons are not the same part used on the Sparkfun board. They're smaller and not as tall, but are at the same position. Third, the pull-up resistance for the qwiic connector is 10k instead of 2.2k, which may limit the maximum I2C clockrate.

![[front]](.pic/front-1200px.jpg)
![[back]](.pic/back-1200px.jpg)

Finally, regarding fabrication. Unlike the Sparkfun board, which uses thin traces and tiny vias. This board is designed for JLCPCB's cheapest 4 layer process. All vias are 0.5mm with 0.3mm drill. USB differential pair is designed for *JLC04081H-3313*, JLC's free tier of impedance controlled boards. Though at 12Mbps, it likely would not have mattered anyway.

By default, this board does not have castellated pads. If your application requires it, replace the footprint for J3 with *12x2 castellated* in the project footprint library. No other modification necessary. Note this will likely incur additional cost for fabrication.

---

# License

The work is released under CC BY-SA 4.0 license.