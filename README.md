# maixbit_tutorials

Tutorials and samples for Maix Bit

This repo is based on [MaixPy official documentation](https://maixpy.sipeed.com/en/).

![](./img/maixbit_yolo_tiny.gif)


# Set up


## Add user in `dialout` group


```bash
sudo adduser $(whoami) dialout
```

After this command, you need to logout and login.

## Connect Maix Bit

Connect Maix Bit, LCD, camera and USB-C like below.

![](https://images-na.ssl-images-amazon.com/images/I/31rwSOhaVDL.jpg)

## Check whether Maix Bit is detected

```bash
ls -alF /dev/ttyUSB*
# /dev/ttyUSB0 might be detected.
```

## Update firmware
### Download latest firmware

Download latest firmware [MaixPy v0.3.2](https://github.com/sipeed/MaixPy/releases/) from [here](https://github.com/sipeed/MaixPy/releases/download/v0.3.2/maixpy_v0.3.2_full.bin).

### Download `kflash_gui`

Download [kflash_gui v1.3.2](https://github.com/sipeed/kflash_gui/releases) from links below.
- [Ubuntu 18.04](http://dl.cdn.sipeed.com/kflash_gui_v1.3.2_linux.tar.xz)
- [Ubuntu 16.04](http://dl.cdn.sipeed.com/kflash_gui_v1.3.2_ubuntu16.tar.xz)

### Run `kflash_gui`

```bash
cd ~/Downloads
tar xvzf kflash_gui_v1.3.2_ubuntu16.tar.xz
cd kflash_gui
./kflash_gui
```

### Burn firmware 

Set `kflash_gui` like below and burn `maixpy_v0.3.2_full.bin` into `Flash`.

![](./img/kflash_gui_burn.png)

## Install and set up `minicom`

### Install `minicom`

```bash
sudo apt install minicom
```

### Set up `minicom`

```bash
sudo minicom -s
```

Set up following settings.
- Serial Device: `/dev/ttyUSB0` 
- Backspace key sends: `DEL` 
- Line wtap: `Yes`

For more detailed information, read [here](https://maixpy.sipeed.com/en/get_started/power_on.html).

### Try `minicom`

```bash
minicom
```

In minicom, you can try import `MaixPy`.

```python
>>> import Maix
>>>
# no error means success.
```

You can also try LED blink test as below.

```python
from Maix import GPIO

fm.register(board_info.LED_R, fm.fpioa.GPIO0)

led_r=GPIO(GPIO.GPIO0,GPIO.OUT)
led_r.value(0)
```

### Finish `minicom`

You can finish `minicom` with  `Ctrl+A X`.

## Install `uPyLoader`

### Download `uPyLoader`

Download `uPyLoader` from [here](https://github.com/BetaRavener/uPyLoader/releases/download/v0.1.4/uPyLoader-linux).

### Install `uPyLoader`

```bash
cd ~/Downloads
mkdir ~/.local/bin
export PATH=$HOME/.local/bin:$PATH
# you can write it in ~/.bashrc
cp ./uPyLoader-linux ~/.local/bin/uPyLoader
uPyLoader
```

## Run display demo

### Clone this repo

```bash
git clone https://github.com/knorth55/maixbit_tutorials.git
```

### Upload `scripts/demo_fps_display.py`

```bash
cd maixbit_tutorials
uPyLoader
```
First click `connect` button to connect `/dev/ttyUSB0`.

Then, select `scripts/demo_fps_display.py` and click `Transfer` button below.

![](./img/upyloader_transfer.png)

### Execute through `minicom`

Run `minicom`

```bash
minicom
```

Then, execute `demo_fps_display.py` as below.

```python
with open('demo_fps_display.py') as f:
    exec(f.read())
```
