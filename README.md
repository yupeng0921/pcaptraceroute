# pcaptraceroute
pcaptraceroute is similiar as traceroute, but generate the probe package from a pcap file. In some special situations, the network only drop some specific type package, for example, a fireware only drop tcp ack package, traceroute can not detect such thing. In this situation, pcaptraceroute can send a specific type package and detect where the package is droped.

## install
pcaptraceroute is a bash script, beofore run it, you should install tcpdump and tcpreplay. For example, in a CentOS system, you should:

    yum install -y tcpdump
	yum install -y tcpreplay

to install tcpreplay, you may install epel repo first:

    rpm -ivh http://mirrors.hustunique.com/epel/6/i386/epel-release-6-8.noarch.rpm

Then get the pcaptraceroute:

    git clone https://github.com/yupeng820921/pcaptraceroute.git

or get the zip file and exact it:

    wget https://github.com/yupeng820921/pcaptraceroute/archive/master.zip
	unzip master.zip

In the pcaptraceroute directory, you will find the pcaptraceroute script and the default pcap package: ack.pcap

## usage
Run the pcaptraceroute on the command line (require root permision):

    ./pcaptraceroute 54.223.129.6
    src_ip: 172.31.13.140
    dst_ip: 54.223.129.6
    src_mac: 02:80:5A:06:33:35
    dst_mac: 06:fa:3a:40:00:01
    device: eth0
    waittime: 5
    nqueries: 3
    sendwait: 0
    max_ttl: 30
    first_ttl: 1
    pcap_package: ack.pcap
    tmp_dir: /tmp/pt_17672_20141113130441
    
    01 ec2-175-41-128-232.ap-southeast-1.compute.amazonaws.com
    02 203.83.223.230
    03 203.83.223.22
    04 203.83.223.3
    05 63-218-107-45.static.pccwglobal.net
    06 202.97.61.89
    07 202.97.61.53
    08 202.97.53.249
    09 202.97.53.41
    10 * * *
    11 42.220.120.106.static.bjtelecom.net
    12 54.222.1.67
    13 54.222.1.91
    14 54.223.129.6

You can specific another pcap file by using the -g option:

     ./pcaptraceroute -g /tmp/another.pcap 54.223.129.6

You can you 'tcpdump -w' capture a pcap file, and use the editcap command exact the specific package from the pcap file. The pcap file followed by -g should be a single tcp pcap file.
