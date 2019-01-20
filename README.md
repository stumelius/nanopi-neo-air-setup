# nanopi-neo-air-setup

This guide describes how to setup a WiFi connection and a rpi-monitor service on a [NanoPi NEO Air](http://nanopi.io/nanopi-neo-air.html).

## Setup WiFi

1. Connect NanoPi NEO Air to your PC with Matrix-USB2UART usb-serial adapter
2. Attach WiFi antenna to the NanoPi
3. Install Python requirements (preferrably in virtualenv): `pip install -r requirements.txt`
3. List available ports: `python -m serial.tools.list_ports`
4. Open NanoPi terminal: `python -m serial.tools.miniterm <port> 115200`
5. Enable wifi and set SSID and password:

        sudo nmcli r wifi on
        nmcli device wifi list
        sudo nmcli device wifi connect SSID password PASSWORD

6. Check the assigned ip with `ifconfig`
7. SSH to the NanoPi `ssh root@nanopi-ip` (password: `fa`)
8. Update packages (may take several minutes):

        apt-get update
        apt-get upgrade

## Install rpi-monitor

1. SSH as root: `ssh root@nanopi-ip` (password: `fa`)
2. Install rpi-monitor:

        wget http://goo.gl/vewCLL -O /etc/apt/sources.list.d/rpimonitor.list
        apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 2C0D3C0F
        apt-get update
        apt-get install rpimonitor

3. Update rpi-monitor: `/etc/init.d/rpimonitor update`
4. Check rpi-monitor status: `service rpimonitor status`
5. Go to `http://nanopi-ip:8888` on your browser

For more information on rpi-monitor installation, see [RPi-Monitor documentation](https://xavierberger.github.io/RPi-Monitor-docs/11_installation.html).

## Useful commands

* Graceful shutdown: `shutdown -h now`
* Check CPU temperature: `cpu_freq`