# LightBrush
C firmware to turn your flashlight into a lightpainting brush.

## How to use
1. Clone this repository
2. Install Docker and download the anduril-builder image from releases.
```shell
docker pull ghcr.io/realdyllon/lightbrush/lightbrush-builder:latest
```
3. Run  
```shell
docker run --rm -v /Users/johndoe/Developer/LightBrush:/src lightbrush-builder sp36-t1616  
# Replace sp36-t1616 with your flashlight's microcontroller.
```
4. Flash your flashlight over serialupdi with the generated .hex file. You can use avrdude or any suitable alternative
```shell
avrdude -p attiny1616 -c serialupdi -P /dev/cu.usbserial-1430 -U flash:w:anduril.sofirn-sp36-t1616.hex
# Replace the params to suit your needs.
```

