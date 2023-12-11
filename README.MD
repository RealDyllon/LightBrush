# LightBrush

An embedded C firmware to turn your flashlight into a lightpainting brush.

This repo is a fork of gabriel_hart's [Anduril2](https://code.launchpad.net/~gabe/flashlight-firmware/anduril2) firmware,
which is a fork of ToyKeeper's [Anduril2](https://code.launchpad.net/~toykeeper/flashlight-firmware/anduril2) firmware.

Toykeeper also maintains a github repo alongside the above-linked launchpad repo, which can be found [here](
https://github.com/ToyKeeper/anduril)

## Setup

> [!NOTE]  
> A linux or mac machine is strongly recommended for building and flashing. If you are on windows, either dual boot to a
linux distro, use WSL2, or a virtual machine.

### Clone this repository

```bash
git clone git@github.com:RealDyllon/LightBrush.git
```

### Install Docker 

Follow the instructions for your operating system [here](https://docs.docker.com/get-docker/).

### Pull the anduril-builder image from releases.

```shell
docker pull ghcr.io/realdyllon/lightbrush/lightbrush-builder:latest
```

Alternatively, you can build the image yourself. 

```shell
cd builder
docker build -t lightbrush-builder .
```

Alternatively, if you really want you can skip docker entirely and use make to build the firmware. Instructions can be 
found at [Toykeeper's GitHub repo README](https://github.com/ToyKeeper/anduril#compiling). A linux machine is strongly 
recommended for this.

### Build the firmware for your flashlight model with the builder image  

If you're building without docker, you can skip this step.

Replace sp36-t1616 with your flashlight's microcontroller.  
Replace johndoe with your username.   
Replace the path with the path to your cloned repository.  

```shell
docker run --rm -v /Users/johndoe/Developer/LightBrush:/src lightbrush-builder sp36-t1616  
```

### Ping your flashlight

Connect your flashing kit to your flashlight and computer.

Replace serial port and microcontroller in the below command as needed.

```shell
 avrdude -p t1616 -c serialupdi -P /dev/cu.usbserial-1430 -n
```

If you get a response like this, you're good to go:  
`avrdude: AVR device initialized and ready to accept instructions`

If you get a connection error, ensure that your flashing kit is working as intended.

### Backup your flashlight's factory firmware

Replace params with your flashlight's model and microcontroller, and serial port.

```bash
avrdude -p attiny1616 -c serialupdi -P /dev/cu.usbserial-1430 -U flash:r:old-anduril.sofirn-sp36-t1616.hex:i
```

This will generate a file called old-anduril.sofirn-sp36-t1616.hex

### Flash your flashlight 

Flash your flashlight over serialupdi with the generated .hex file. You can use avrdude or any other alternative

```shell
# Replace the params to suit your needs.
avrdude -p attiny1616 -c serialupdi -P /dev/cu.usbserial-1430 -U flash:w:lightbrush.sofirn-sp36-t1616.hex
```

## License

This project is licensed under the GPL v3 license. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

* [ToyKeeper (Selene Scriven)](https://launchpad.net/~toykeeper)
* [Gabriel_Hart](https://launchpad.net/~gabe)
