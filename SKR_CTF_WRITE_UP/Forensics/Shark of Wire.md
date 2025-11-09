# CTF Write-Up: Extracting the Flag from a PCAP File

## Overview
The challenge provided a PCAP file, which is a network traffic capture file containing a history of packets exchanged over the network during a session.

## Steps to Solve

1. **Open Wireshark**
   - If Wireshark is not installed, download and install it from [wireshark.org](https://www.wireshark.org/).

2. **Load the PCAP file**
   - Launch Wireshark.
   - Go to `File` > `Open` and select the downloaded PCAP file.

3. **Inspect the traffic**
   - Use the inspection pane to view all captured packets.

4. **Apply HTTP filter**
   - In the filter bar, type `http` and press Enter to filter only HTTP traffic.

5. **Find the flag**
   - Look for an HTTP packet with a response containing text/html content.
   - In this case, the flag was found in packet number 182 with the following details:
     - Time: 77.670534 seconds
     - Source IP: 172.25.0.2
     - Destination IP: 172.25.0.3
     - Protocol: HTTP
     - Info: `HTTP/1.1 200 OK (text/html)`

6. **View the flag in the packet details**
   - The HTTP response includes the line:
     ```
     <h1>Flag: SKR{0pen_Pcap_File_1n_Wir3Sh4rk}</h1>
     ```
