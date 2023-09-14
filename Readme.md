# Hardware Boot Selection Switch Using WAVESHARE RP2040 ZERO

Inspired by Hackaday.io project(https://hackaday.io/project/179539-hardware-boot-selection-switch)  
Check Steps in Hackster.io: https://www.hackster.io/Madrajib/hardware-boot-select-switch-using-pico-a3e3d5

### make the project
```bash
$ git clone this project
$ cd HARDWARE_BOOT_SELECTION_SWITCH

$ mkdir build
$ cd build
$ cmake -DPICO_BOARD=waveshare_rp2040_zero ..
$ make
```
Now Copy the pico_msd.uf2 file to rp2040 zero

POSSIBLE PROBLEM WITH RP2040 ZERO: 
* https://github.com/hathach/tinyusb/issues/1730
* https://github.com/raspberrypi/pico-sdk/pull/1421

TEMPORARY SOLUTION: 
* https://github.com/raspberrypi/pico-sdk/issues/1304

### In Ubuntu edit the grub file:
```bash
$ sudo vim /etc/grub.d/40_custom

search --no-floppy --fs-uuid --set hdswitch 0000-1234
if [ "${hdswitch}" ] ; then
  source ($hdswitch)/switch.cfg

  if [ "${os_hw_switch}" == 0 ] ; then
    # Boot Linux
    set default="0"
    set timeout=0
  elif [ "${os_hw_switch}" == 1 ] ; then
    # Boot Windows
    set default="1"
    set timeout=0
  elif [ "${os_hw_switch}" == 2 ] ; then
    # Boot Otro
    set default="2"
    set timeout=0    
  else
    # Fallback to default
    set default="${GRUB_DEFAULT}"
  fi

else
  set default="${GRUB_DEFAULT}"
fi

```
