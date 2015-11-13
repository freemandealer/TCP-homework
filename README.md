# TCP-homework

This is a instruction for the TCP course homework.

#Prepare 
This homework is based on a TCP diagnosis tool tapo. Tapo is a TCP performance diagnosis tool. It runs on Linux.
We have made some changes in tapo, so you can get results for this homework directly.
You can get it by:  `git clone https://github.com/zhoujianer/TCP-homework.git`
To build it, you need to install libpcap libraries(in ubuntu use this command: `sudo apt-get install libpcap-dev`).


#Download flow analysis 
1 Configure a laptop as an AP(access point). The WeChat flows should go through that laptop.

2 Running Wireshark on the laptop to capture all the flows that go through it when you're downloading video from WeChat, and get a pcap file all.pcap.

3 Analyze all.pcap by Wireshark, and try to find the TCP flow caused by downloading the video. Suppose the download flow’s source ip and port are 116.211.111.227:80(WeChat server), destination ip and port are 172.16.32.2:49273(your phone)

4 Filter the download video flow. Using this  command to filter it(in Linux):

    tcpdump -r all.pcap host 172.16.32.2 and port 49273 -w ./download.pcap

5 Using tapo to analyze the download.pcap:

    ./tcp_tool -f download.pcap -s 116.211.111.227 -p 80 -t down > download.txt

You will see the sequence number and packet reorder rate from 'download.txt'.


#Upload flow analysis
1 The same way to capture all the flows when you upload video to WeChat.

2 Analyze all.pcap by Wireshark, and try to find the TCP flow that upload video to WeChat. Suppose the upload flow’s source ip and port are 172.16.32.2:49275(your phone), destination ip and port are 116.211.111.227:80(WeChat server).

3 Filter the upload video flow. Using this command to filter it(in Linux):

tcpdump -r all.pcap host 172.16.32.2 and port 49275 -w ./upload.pcap

4 Using tapoo to analyze the upload.pcap:

./tcp_tool -f upload.pcap -s 172.16.32.2 -p 49275 -t up > upload.txt

You will see the sequence number, inflight number and packet loss rate from 'upload.txt'.


