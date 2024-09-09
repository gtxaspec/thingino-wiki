## PWM Control

The `pwm-ctrl` utility is a command-line tool that facilitates the control of pulse-width modulation (PWM) on specific GPIO pins. PWM is commonly used for adjusting the brightness of LEDs.

### Usage
The command syntax for the `pwm-ctrl` utility is as follows:

```shell
root@ing-teacup-2a10 # /sbin/pwm-ctrl [-l] <gpio> <brightness 0-100>
```

Where:
- `-l`: Lists all available PWM-capable GPIOs on the system.
- `<gpio>`: Specifies the GPIO number for PWM control.
- `<brightness 0-100>`: Sets the brightness level from 0 (off) to 100 (maximum brightness).

### Listing PWM Capable GPIOs
To find out which GPIO pins are capable of PWM, you can use the `-l` option. This will display a list of all the PWM-capable GPIOs along with their corresponding labels and pin numbers:

```shell
root@ing-teacup-2a10 # pwm-ctrl -l
Available PWM-capable GPIOs:
GPIO 46 = PWM0 (PA14)
GPIO 54 = PWM1 (PA22)
GPIO 49 = PWM0 (PB17)
GPIO 50 = PWM1 (PB18)
GPIO 59 = PWM2 (PB27)
GPIO 60 = PWM3 (PB28)
```

### GPIO Compatibility
It is important to note that PWM control can only be applied to GPIOs that support PWM functionality. Attempting to use the `pwm-ctrl` command on non-PWM-capable GPIOs will not work, as these pins do not support the function necessary for varying power outputs.

### Controlling Brightness
Once you have identified the correct GPIO pin from the list, you can control the brightness by specifying the GPIO number and the desired brightness level. For example, to set the brightness of GPIO 46 to 50%:

```shell
root@ing-teacup-2a10 # pwm-ctrl 46 50
```
