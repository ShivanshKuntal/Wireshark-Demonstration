
# HTTP Request Analysis Using Wireshark  
**Submitted by:** Shivansh Kuntal  
**Practical Title:** Analysing a Simple HTTP Request with Wireshark  

---

## 📌 Overview  
This experiment demonstrates how to capture, filter, and analyze plaintext HTTP traffic using Wireshark.  
The goal is to understand the structure of HTTP requests and responses, identify network endpoints, and observe protocol-level behavior at the packet layer.

---

## 🧰 Tools Used  
- **Wireshark** – Packet sniffer and protocol analyzer  
- **Web Browser** – Used for generating HTTP traffic (http://example.com)

---

## 🧠 Part A – Theoretical Concepts  

### **1. What is Wireshark?**  
Wireshark is an open-source network protocol analyzer used to inspect packets in real time or from saved captures.  
It reveals packet headers, payloads, conversations, and protocol flows, making it indispensable for network engineers and security analysts.

#### Key Features  
- Real-time and offline packet capture  
- Decoding of hundreds of protocols  
- Detailed packet dissection  
- Capture & display filtering  
- Statistical views (conversations, flow graphs, protocol hierarchy)  
- Cross-platform support  

#### Common Use Cases  
- Troubleshooting latency, packet loss, and protocol errors  
- Security investigation of suspicious or malicious network activity  
- Learning and analyzing network protocols  
- Forensics and incident reconstruction  

---

### **2. Types of Wireshark Filters**

#### **Capture Filters**  
Applied *before* capture; restrict what Wireshark stores.  
Uses **BPF syntax**.  
Examples:  
- `host 192.168.1.1`  
- `port 80`  

#### **Display Filters**  
Applied *after* capture; refine what is shown in the UI.  
Uses Wireshark’s own filter language.  
Examples:  
- `http`  
- `ip.src == 10.0.0.5 && tcp.port == 443`

---

### **3. Wireshark in Cybersecurity**  
Wireshark is widely used for threat hunting and digital forensics because it exposes packet-level data.

Key security applications:  
- Detecting anomalous hosts or suspicious protocols  
- Tracing attacker activity and reconstructing events  
- Investigating malware traffic and C2 communication  
- Ensuring sensitive data is not transmitted in plaintext  
- Identifying rogue devices (fake DNS/DHCP servers)

---

## 🧪 Part B – Practical Implementation  

### **Objective**  
- Capture an HTTP request/response  
- Identify client and server IPs  
- Extract key HTTP metadata  
- Understand packet-level behavior  

---

## 🔧 Procedure  

### **1. Start Packet Capture**  
- Open Wireshark  
- Select active interface (Wi-Fi/Ethernet)  
- Begin capture  

### **2. Generate HTTP Traffic**  
Open a browser and visit:  
```
http://example.com
```
Using HTTP ensures the packet contents are unencrypted and readable.

### **3. Stop Capture**  
Stop recording once the page loads.

### **4. Apply Display Filter**  
Use the filter:  
```
http
```
This isolates only HTTP packets for analysis.

---

## 📑 Analysis  

### **1. Identify HTTP Request Packet**  
Find:  
```
GET / HTTP/1.1
```

### **2. Source & Destination IP Addresses**  
From the IPv4 header:  
- **Source IP:** Your machine (example: `192.168.1.5`)  
- **Destination IP:** Web server (`93.184.216.34`)

### **3. HTTP Request Details**  
Expand **Hypertext Transfer Protocol** section:  
- Host: `example.com`  
- User-Agent: Browser identification  
- Accept headers  

### **4. HTTP Response Analysis**  
Locate the `HTTP/1.1 200 OK` packet:  
- Status Code: 200  
- Content-Type: `text/html`  
- Server: e.g., `ECS`  
- Content-Length: size of HTML payload  

---

## 🔍 Key Observations  
- HTTP (non-HTTPS) traffic is fully readable in plaintext.  
- Both headers and content can be inspected directly.  
- IP addresses and metadata help map client-server communication.  
- Visibility of Host, User-Agent, and Accept headers shows how much information a browser leaks during normal browsing.

---

## 📘 TCP Handshake Summary  
From the recorded packets:  
- SYN  
- SYN-ACK  
- ACK  

Total packets for the handshake: **3**

Total SYN packets observed during capture: **18** (due to multiple reconnect attempts or background traffic)

---

## ✅ Conclusion  
This experiment demonstrates how Wireshark can be used to:  
- Capture and isolate HTTP traffic  
- Identify client and server endpoints  
- Inspect HTTP headers and content  
- Understand request/response behavior  
- Observe TCP handshake patterns  

Such analysis is foundational for:  
- Network troubleshooting  
- Web debugging  
- Security monitoring  
- Digital forensics  




