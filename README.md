## How to flash Achilles Pro firmware on Eachine Pro58 on a mac using ST-Link v2


1. Install brew
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Install stlink and openocd and telnet
```
$ brew install openocd
$ brew install telnet
```

3. Convert the hex file to binary using `arm-none-eabi-objcopy` (make sure the binary is in your $PATH)
```
$ arm-none-eabi-objcopy -I ihex --output-target=binary <path>/Achilleas_V_1_4_EACHINE.hex  <path>/achilles.bin
```

4. Run openocd
```
$ openocd -f openocd.cfg -f stm32f1x.cfg -c init
```

5. Open another terminal and use telnet to connect to the debugger
```
$ telnet localhost 4444
```

6. Make sure your module is connected
```
> targets
```

7. Halt the module
```
> halt
```

8. Unlock the flash (if needed)
```
> stm32f1x unlock 0
```

9. Reset to apply the changes
```
> reset run
```

10. Halt again
```
> halt
```

11. Erase bank 0
```
> stm32f1x mass_erase 0
```

12. Flash the binary
```
> flash write_bank 0 <absolute_path>/achilles.bin 0
```

13. Reset the module
```
> reset run
```
