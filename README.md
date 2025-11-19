# minix-custom-tcpip-stack



Course: SPD (Secure Protocol Design)
Admin: Sumit Soni
---

📌 1. Objective of the Assignment

The purpose of this experiment is to design and implement a custom minimal TCP/IP protocol stack on top of Minix OS and verify packet transmission using Wireshark/Tshark.

This includes:

* Understanding TCP/IP protocol layering
* Implementing minimal versions of Ethernet, IPv4/IPv6, ICMP, UDP/TCP
* Creating a pipelined 4-layer protocol stack
* Sending packets over a TAP/NIC interface
* Capturing packets in Wireshark and attaching screenshots to GitHub

---

📌 2. Protocol Stack Requirements (Given in Assignment)

✔ Application Layer

Implements:

* DHCP
* HTTP
* SMTP

✔ Transport Layer

Supports:

* TCP
* UDP

✔ Internet Layer

Supports:

* IPv4 / IPv6
* ICMP (Echo Request/Echo Reply)

✔ Ethernet Layer (Link Layer)

Implements:

* Ethernet II framing
* Works with NIC / TAP device
* Sends raw frames over the wire
* Packets must be detectable in Wireshark

---

📌 3. Tools Used

* Minix OS
* Python 3
* TAP Interface (Linux/Kali)
* Wireshark / Tshark
* Git & GitHub
* VS Code / Nano Editor

---

📌 4. Folder Structure (Project Repository)

```
minix-tcpip-stack/
│
├── README.md
├── src/
│   ├── link.py
│   ├── internet.py
│   ├── transport.py
│   └── application.py
│
├── examples/
│   └── run_demo.py
│
└── docs/
    ├── capture.pcapng
    ├── handwritten_lab_page.pdf
    └── wireshark_screenshots/
```

---

📌 5. How the Stack Works (Simple Explanation)

1️⃣ Application Layer

Creates demo messages such as:

* DHCP Discover
* HTTP GET
* SMTP HELO

These are passed down to the transport layer.

---

2️⃣ Transport Layer

* Encodes data using **UDP** or **TCP** headers
* Adds ports and checksum placeholders

---

3️⃣ Internet Layer

Wraps transport-layer data inside **IPv4 / IPv6** packets
Adds:

* Version
* Header length
* TTL
* Protocol number
* Source & Destination IP

Also supports ICMP Echo Request/Reply.

---

4️⃣ Ethernet Layer (Link Layer)

Creates an Ethernet II frame containing:

* Destination MAC
* Source MAC
* EtherType
* IP payload

Sends frame through a TAP interface in Linux/Kali.

---

📌 6. How to Run the Demo (Linux/Kali)

Step 1 — Create TAP interface

```bash
sudo ip tuntap add dev tap_demo0 mode tap
sudo ip link set dev tap_demo0 up
sudo ip addr add 192.168.100.2/24 dev tap_demo0
```

Step 2 — Run demo Python script

```bash
sudo python3 examples/run_demo.py
```

This creates & sends:

* Ethernet II frame
* IPv4 header
* ICMP Echo packet

---

📌 7. Packet Capture & Verification

1. Open Wireshark
2. Select interface **tap_demo0**
3. Run the demo script
4. Wireshark displays:

   * Ethernet II
   * IPv4
   * ICMP Echo Request

Screenshots stored in:

```
docs/wireshark_screenshots/
```

---

📌 8. Handwritten Work

A handwritten page includes:

* Aim
* Theory
* TCP/IP 4-layer diagram
* Steps
* Conclusion

Uploaded as:

```
docs/handwritten_lab_page.pdf
```

---

📌 9. GitHub Submission Steps

```
git init
git add.
git commit -m "Initial TCP/IP stack submission"
git branch -M main
git remote add origin https://github.com/<your-username>/minix-tcpip-stack.git
git push -u origin main
```

---

📌 10. Output Files Included

* ✔ Packet capture file: `capture.pcapng`
* ✔ Wireshark screenshots
* ✔ Python implementation skeleton
* ✔ Handwritten PDF
* ✔ README documentation

---

📌 11. Conclusion

This experiment demonstrates the architecture of a **custom TCP/IP stack**, covering:

* Application → Transport → Internet → Ethernet pipeline
* How packets are manually constructed
* How TAP interfaces send raw frames
* How analyzers like Wireshark detect packets

It provides a foundational understanding of protocol design & network internals.

---
