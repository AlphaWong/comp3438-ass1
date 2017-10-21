# comp3438-ass1

# Install Buzzer driver
## Step
1. Move the buzzer_driver.c to ```tiny6410/linux-3.08/drivers/char```
1. Add following statement in ```tiny6410/linux-3.08/drivers/char/Makefile```
```
# Remember the file name must be same as step 1 file name.
obj-$(CONFIG_BUZZERDRIVER) += buzzer_driver.o
```
1. Add following statement in ```tiny6410/linux-3.08/drivers/char/Kconfig```
```
config
  tristate "BUZZERDRIVER"
  depends on CPU_S5PV210
```

