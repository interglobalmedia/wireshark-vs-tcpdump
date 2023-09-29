# Wireshark vs tcpdump

First, in order to be able to compare Wireshark tot tcpdump, I had to install them.

I already had the command line tool tcpdump installed. So tcpdump was ready to use. However, I did not have Wireshark installed. I first tried to install it via Homebrew, but that does not seem to work anymore. Besides, I found on the Wireshark site that with Apple Silicon, it is better to install the binary off the official site anyway. So I did.

However, it is a two step process to install Wireshark on macOS.

First, I downloaded the "macOS Arm Disk Image" from the official wireshark.org website, clicked on the the `Wireshark 4.0.8 Arm 64.dmg` to install it, and then dragged the app into the "Applications" folder on my Mac.

Second, as per Wireshark when I first launched it, I found that I also had to install the [“ChmodBPF” launch daemon](https://www.wireshark.org/docs/wsug_html_chunked/ChBuildInstallOSXInstall.html). As per the official documentation, this is necessary in order to be able to be able to capture packets. Kind of important then, right? Especially since that is the whole point of Wireshark!

Once I installed “ChmodBPF”, then the error went away.

Specifically, we need to install "ChmodBPF" in order for the application to [get access to local interfaces](https://condor.depaul.edu/~elliott/435/hw/wireshark/WireSharkTips.html). 

"ChmodBPF" comes from the libcap project and is a piece of software that sets up permissions for users to capture network packets.

According to [condor.depaul.edu](https://condor.depaul.edu/~elliott/435/hw/wireshark/WireSharkTips.html),

>Fortunately, ChmodBPF is packaged with the installer. However, it is a separate step. Once you open Wireshark, there is a link to install it and the installer will run.

tcpdumnp, on the other hand, comes [pre-installed with macOS](https://developer.apple.com/documentation/network/recording_a_packet_trace). FYI: On macOS, [packet captures are also referred to as packet traces](https://success.trendmicro.com/dcx/s/solution/TP000085625-What-is-the-difference-between-a-Packet-Trace-and-a-Packet-Capture?language=en_US&sfdcIFrameOrigin=null). More information about packet traces on macOS can be accessed via the article entitled [Recording a Packet Trace](https://developer.apple.com/documentation/network/recording_a_packet_trace) on `developer.apple.com`.

$$ Main differences between Wireshark and tcpdump

- The first difference between Wireshark and tcpdump for me? tcpdump is a pre-installed tool on macOS. Wireshark is not.

- Wireshark is a graphic user interface, whereas tcpdump is a command line interface (CLI) tool. Wireshark's graphical user interface provides a user friendly experiences, and it has advanced features such as real-time analysis and fitering. tcpdump is ideal to run in remote servers or devices for which a GUI is not available, to collect data that can be analyzed later.

- tcpdump is lightweight and can be used on servers without a graphical user interface. This makes it a great choice for network administrators who [need to monitor remote servers](https://skillsstreet.com/mainframe-vs-server/). On the other hand, Wireshark is typically deployed on workstations insgtead of servers, because it comes with a GUI that offers more advanced features and greater flexibility.

- tcpdump has a greater learning curve because it requires a solid understanding of syntax and commands, which can be intimidating to beginners. On the other hand, Wireshark's visual interface is more user friendly, and might be preferred by those less familiar with networking concepts.

- Wireshark can capture traffic and decode the messages which can be saved to a file to an understandable format for the user to find the reasons of poor performance, intermittent connectivity, etc. On the other hand, tcpdump output saved to files are not easily understandable to the user.

- Wireshark is both a packet sniffer and analyzer. Wireshark offers a wide range of analysis features with its powerful tool set. With color coding, filters, and protocol dissectors, it has the ability to reassemble and follow streams, providing in-depth analysis of packets. tcpdump, on the other hand, is limited in its analysis capabilities, so it works more as a traffic capturing tool and not an analyzer. It displays packet data directly in Terminal. So if you want deep traffic analysis and troubleshooting, Wireshark is the tool to go with.

- Wireshark displays all the data inside the packet but TCPdump only shows information in packet headers. It does not display all the data inside the packet.

- TCPdump can only show the information of TCP/IP based packets and does its job well. While Wireshark is much more versatile and can interpret and show different protocols.

- TCPdump has problems with some commands working with IPv6 packets. As a result, IPv6 users should use Wireshark.

## Main similarities between Wireshark and tcpdump

- Both Wireshark and tcpdump are open source software projects, and therefore free.

- Both Wireshark and tcpdump are compatible with different types of operating systems such as Linux, Solaris, FreeBSD, NetBSD, OpenBSD, Mac OS X, other Unix-like systems, and Windows.

- Like Wireshark, TCPdump also has a good filtering language to capture only the desired packets that match a specified filter.

- Neither Wireshark nor TCPdump function as an intrusion detection system.

- Wireshark and tcpdump both cannot generate alarms or hints when an active or passive attack or strange behavior happens on the network. However, they might help the analyst find out what is really going on inside the network.

- Both oWireshark and tcpdump can only be used to measure or capture information.

- The captured file format for both Wireshark and tcpdump is in “libpcap” format.