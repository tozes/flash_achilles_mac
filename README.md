## How to flash Achilles Pro firmware on Eachine Pro58 on a mac using ST-Link v2


1. Install brew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Install stlink and openocd and telnet
```
brew install openocd
brew install telnet
```

3. Convert the hex file to binary using `arm-none-eabi-objcopy` (make sure the binary is in your $PATH)
```
arm-none-eabi-objcopy -I ihex --output-target=binary <path>/Achilleas_V_1_4_EACHINE.hex  <path>/achilles.bin
```

4. Run openocd
```
openocd -f openocd.cfg -f stm32f1x.cfg -c init
```

5. Use telnet to connect to the debugger
```
telnet localhost 4444
```

6. Make sure your module is connected
```
> target
```

7. Unlock the flash (if needed)
```
> stm32x_unlock 0
```

8. Flash the binary
```
flash write_bank 0 <absolute_path>/achilles.bin 0
```
