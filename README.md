![p1](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/bamboozled2.png?token=f2076a998e726ed1c0602cca487ec3d9d8c402e5)
### Ludovic Blunat, Stanislas Bruhière, Renan Herniou
CentraleSupélec Rennes, academic year 2016/2017

![p2](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/cover.jpeg?token=f068a968103ada07db1aded7012c03808fae53b9)

## How does addressable LEDs work?
First of all, we focus on the behavior of an addressable LED strip such as the one used in this project (with WS2812 RGB LEDs). Why such a component? Because it is cheap and available in several configurations (LEDs density, waterproof or not, etc.). Strips used in this project [1] have 3 pins: ground, 5V and a data pin.

![p3](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/led_strip.png?token=dbcb78339da97e1423e5a90462fa884098302944)

A single strip is connected to an Arduino board which sends 8-bit RGB and intensity values. Fortunately for us, we do not have to dive at the register level to control such a component: Adafruit has published a library online: https://github.com/adafruit/Adafruit_NeoPixel.

Each WS2812 LED includes a microcontroller processing the data signal; first 3 bytes are taken into account by the LED cell; then, the microcontroller sends remaining bytes to the next LED. Each WS2812 can be seperated from others; furthermore, we can solder power/signal pins to create a custom layout without breaking the transmission between all LEDs.

An LED is an optoelectronic component: it is able to produce light when powered by an electric current. Unlike incandescent light bulbs, an LED does not contain a filament but several semiconductors layers. These semiconductors (aluminium nitride `AlN` and gallium phosphate `GaPO_4`) do not create current resistance nor energy loss when emitting light.

When an electric current crosses semiconductor layers, many electrons encounter positively charged atoms creating energy as a light flux. The light flux is nearly monochromatic due to a small transmission bandwidth. We can play with the light wavelength by modifying semiconductor layers. Several semiconductor technologies are available on the market. A RGB LED consists of 3 seperate cells emitting at 3 wavelengths (for red, green and blue). The microcontroller embedded in the WS2812 chip adjusts the voltage for each monochromatic cell in order to vary the intensity and the overall color emitted by the WS2812.

![p4](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/global.png?token=622d3ea46238a53584f9690043e6db70e72a5669)

## Project description
We have built a 16x16 LED panel which can be controlled by an Arduino. Each LED can be controlled individually: therefore, we are able to create animations on the panel.

### Power supply
In such a project, the power supply is not the easiest part: in fact, during our first test phasis, we have seen that current consumption was quite high. After several searches, it turns out that the maximum current by a RGB LED is about 60 mA (20mA for each subpixel). In the worst case (each pixel transmitting a white light at maximum brightness), BamboozLED<sup>TM</sup> could consume up to 255x0.05=15.36A!
* First, we thought to use a computer power supply: unfortunately, it did not deliver enough current and turned off into a secured mode before it shut down. BamboozLED<sup>TM</sup> was bamboozled :|
* Then, we looked for 5V power supply: however, 5V with high current features are \textbf{really} rare. In other words, it was nearly impossible to find it...

Finally, we chose a 12V power supply. We needed to lower the input voltage to 5V using a Buck boost converter [2,3]. However, such converters rarely deliver more than 10A. The trick consisted in dividing the LED panel in two parts: each part has its own Buck boost converter.

### Structure
The frame of BamboozLED<sup>TM</sup> is made of 10mm-wide wood panels, its whole size is a parallelepipoid of 540x540x30mm.

![p5](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/pic1.jpg?token=c478e7035b94e4e8632239c40f366e6d99efefe3)
![p6](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/pic2.jpg?token=a5d42d62a40c8fd6caadc0f6f3723cd4454e5cd9)

Due to the light intensity, we decided to put a 3mm transparent PVC layer at the top. Furthermore, we also put opaque PVC layers between each pixel.

The 16 LED strips (including 16 LEDs each) are linked in a "snake"' layout to transmit the data signal all along BamboozLED<sup>TM</sup>. The data signal is extended towards the Arduino driving the LED panel.

### Software
In order to control the animation running on BamboozLED<sup>TM</sup>, we used Glediator [4]: this software offers several possibilities through its interface: pictures mixing, colors effects... The greatest feature of Glediator is the ability to modify how the signal is trasmitted to the Arduino depending of the layout of the target panel (we can specify panel dimensions, we can use a set of several panels, etc.).

![p7](https://bytebucket.org/pcotret/bamboozled/raw/e0ce517bc1800941d1e6d031656f7b37c84bef6c/report/img/glediator.jpg?token=004f93e2ab35450cecba4bad15fca44aa9293b79)

## Arduino code
https://bitbucket.org/pcotret/bamboozled/src/e0ce517bc1800941d1e6d031656f7b37c84bef6c/WS2812_Glediator/?at=master

This link contains a sample code that has been generated by Glediator.

## Perspectives
BamboozLED<sup>TM</sup> is finally a low-cost RGB LED panel that can be used as a geeky decoration or as a f###### great screen for student parties. For BamboozLED<sup>TM</sup> v2.0, we plan to create several panels which can be associated and more or less automatically detected by the microcontroller driving the whole circuit. Basically, something like [5] but much cheaper!

## References
1. BTF-LIGHTING, "BTF-LIGHTING WS2811 150leds 30pixels PCB noir", http://amzn.to/2tDvaoH.
2. LAOMAO, "LAOMAO Régulateur de tension DC-DC 4,5-30V à 0.8-30V 12A convertisseur
de tension réglable Step Down Convertisseur", http://amzn.to/2uQO4Ys.
3. SALAR, "Bloc d’alimentation Salcar (12V 10A) 120W, transformateur pour: guirlande
LED 5050", http://amzn.to/2upLcRF.
4. SolderLab, "Glediator", http://www.solderlab.de/index.php/software/glediator.
5. Nanoleaf, "Aurora Smarter Kit [Energy Class A+]", http://amzn.to/2gWVK6g.