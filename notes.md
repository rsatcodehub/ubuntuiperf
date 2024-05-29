### Ubuntu which has access to internet

source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts"
    version   = "latest"
  }
}

mkdir iperf3_packages
cd iperf3_packages

apt-get download iperf3
apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends iperf3 | grep "^\w")
### Compress
tar -cvf iperf3_packages.tar
### Uncompress
tar -xvf iperf3_packages.tar

#### Install
sudo dpkg -id *.deb

#### Validate if iperf3 is running as a server

ps -aux | grep 'iperf3 -s'

#### iperf service - Not needed as sudo systemctl enable iperf3 and sudo systemctl start iperf3 seems to work fine
### Create new service

sudo nano /etc/systemd/system/iperf3.service

Add the following content:

[Unit]
Description=iPerf3 Server

[Service]
ExecStart=/usr/bin/iperf3 -s

[Install]
WantedBy=multi-user.target


##

sudo systemctl daemon-reload

sudo systemctl enable iperf3
sudo systemctl start iperf3

sudo systemctl status iperf3

#########
