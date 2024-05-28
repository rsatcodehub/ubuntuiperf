### Ubuntu which has access to internet

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
