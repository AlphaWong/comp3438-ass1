# comp3438-ass1

# Make linux with Buzzer driver
## Step
1. Move the buzzer_driver.c to ```tiny6410/linux-3.08/drivers/char```
1. Move the button-driver.c to ```tiny6410/linux-3.08/drivers/char```
1. Add following statement in ```tiny6410/linux-3.08/drivers/char/Makefile```
```
# Remember the file name must be same as step 1 file name.
obj-$(CONFIG_BUZZERDRIVER) += buzzer-driver.o
obj-$(CONFIG_BUTTONDRIVER) += button-driver.o
```
1. Add following statement in ```tiny6410/linux-3.08/drivers/char/Kconfig```
```
config
  tristate "BUZZERDRIVER"
  depends on CPU_S5PV210
config
  tristate "BUTTONDRIVER"
  depends on CPU_S5PV210
```

# Mount path of nfs
```bash
mount -t nfs -o nolock,rsize=4096,wsize=4096 192.168.1.145:/tiny6410 /mnt/nfs
```

# Map driver
1. Load driver
```bash
insmod buzzer_driver.ko
```
1. Lockup ports
```bash
cat /proc/devices
```
1. Map to /dev dir
```bash
mknod /dev/buzzer c 250 1
```

# Code
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/ioctl.h>
#include <fcntl.h>

char beep;
int fd;

int main()
{
	fd = open("/dev/buzzer", O_WRONLY);
	if(fd == -1)
	{
		printf("Fail to open device lab4!\n");
		goto finish;	
	}
	while(1)
	{
    write(fd, "0", 1);
	}
	close(fd);

finish:	
	return 0;
}

```
