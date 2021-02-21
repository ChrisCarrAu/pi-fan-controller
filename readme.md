# Raspberry Pi 4 Fan Controller

Turns a 5V fan connected to a selected GPIO port on when the temperature reaches a threshold. It turns it off again when a lower threshold is reached.

Particulary good if you don't want a noisy fan to be on all the time.
## Prerequisites
- Python
- GPIO library

## CODE
### fancontrol.sh
Used to start and stop the fan-controller program.
Note that my fan controller uses pin 7 (GPIO4). If you are using a different pin, you will need to change this setting
Note also that my fan will turn on at 65C and will turn off again when it drops below 55C.

### fan-controller.py


# Setup
Clone this repository to your Pi

Copy the program into your local programs folder and mark it executable

```
sudo mv fan-controller.py /usr/local/bin/
sudo chmod +x /usr/local/bin/fan-controller.py
```

Now move the shell script and make it executable
```
sudo mv script/fancontrol.sh /etc/init.d/
sudo chmod +x /etc/init.d/fancontrol.sh
```
tell your Pi you want the script to run after boot
```
sudo update-rc.d fancontrol.sh defaults
```
Now, either reboot or just start the script
```
sudo reboot
```
or
```
sudo /etc/init.d/fancontrol.sh start
```

# Testing

I used stress-ng to put load into the Pi. Install it with
```
sudo apt install stress-ng mesa-utils
```
and put load onto the CPU with this command
```
stress-ng --cpu 0 --cpu-method fft
```
