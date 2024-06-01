# Cybersecurity Incident Report - DDoS (SYN Flood Attack)
## SCENARIO
You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like. 

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor. 

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

## LOG DATA
| Color | No. | Time       | Source       | Destination  | Protocol | Info                                          |
|-------|-----|------------|--------------|--------------|----------|-----------------------------------------------|
| red   | 52  | 3.390692   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 53  | 3.441926   | 192.0.2.1    | 203.0.113.0  | TCP      | 443->54770 [SYN ACK] Seq=0 Win-5792 Len=120...|
| red   | 54  | 3.493160   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [ACK Seq=1 Win=5792 Len=0...       |
| green | 55  | 3.544394   | 198.51.100.14| 192.0.2.1    | TCP      | 14785->443 [SYN] Seq=0 Win-5792 Len=120...    |
| green | 56  | 3.599628   | 192.0.2.1    | 198.51.100.14| TCP      | 443->14785 [SYN ACK] Seq=0 Win-5792 Len=120...|
| red   | 57  | 3.664863   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 58  | 3.730097   | 198.51.100.14| 192.0.2.1    | TCP      | 14785->443 [ACK] Seq=1 Win-5792 Len=120...    |
| red   | 59  | 3.795332   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win-5792 Len=120...    |
| green | 60  | 3.860567   | 198.51.100.14| 192.0.2.1    | HTTP     | GET /sales.html HTTP/1.1                      |
| red   | 61  | 3.939499   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win-5792 Len=120...    |
| green | 62  | 4.018431   | 192.0.2.1    | 198.51.100.14| HTTP     | HTTP/1.1 200 OK (text/html)                   |
| green | 63  | 4.097363   | 198.51.100.5 | 192.0.2.1    | TCP      | 33638->443 [SYN] Seq=0 Win-5792 Len=120...    |
| red   | 64  | 4.176295   | 192.0.2.1    | 203.0.113.0  | TCP      | 443->54770 [SYN ACK] Seq=0 Win-5792 Len=120...|
| green | 65  | 4.255227   | 192.0.2.1    | 198.51.100.5 | TCP      | 443->33638 [SYN ACK] Seq=0 Win-5792 Len=120...|
| red   | 66  | 4.256159   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 67  | 5.235091   | 198.51.100.5 | 192.0.2.1    | TCP      | 33638->443 [ACK] Seq=1 Win-5792 Len=120...    |
| red   | 68  | 5.236023   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 69  | 5.236955   | 198.51.100.16| 192.0.2.1    | TCP      | 32641->443 [SYN] Seq=0 Win-5792 Len=120...    |
| red   | 70  | 5.237887   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 71  | 6.228728   | 198.51.100.5 | 192.0.2.1    | HTTP     | GET /sales.html HTTP/1.1                      |
| red   | 72  | 6.229638   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| yellow| 73  | 6.230548   | 192.0.2.1    | 198.51.100.16| TCP      | 443->32641 [RST ACK] Seq=0 Win-5792 Len=120...|
| red   | 74  | 6.330539   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 75  | 6.330885   | 198.51.100.7 | 192.0.2.1    | TCP      | 42584->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 76  | 6.331231   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| yellow| 77  | 7.330577   | 192.0.2.1    | 198.51.100.5 | TCP      | HTTP/1.1 504 Gateway Time-out (text/html)     |
| red   | 78  | 7.331323   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| green | 79  | 7.340768   | 198.51.100.22| 192.0.2.1    | TCP      | 6345->443 [SYN] Seq=0 Win=5792 Len=0...       |
| yellow| 80  | 7.340773   | 192.0.2.1    | 198.51.100.7 | TCP      | 443->42584 [RST ACK] Seq=1 Win-5792 Len=120...|
| red   | 81  | 7.340778   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 82  | 7.340783   | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 83  | 7.439658   | 192.0.2.1    | 203.0.113.0  | TCP      | 443->54770 [RST ACK] Seq=1 Win=5792 Len=0...  |
| red   | 119 | 19.198705  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 120 | 19.521718  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| yellow| 121 | 19.844731  | 192.0.2.1    | 198.51.100.22| TCP      | 443->6345 [RST ACK] Seq=1 Win-5792 Len=120...|
| yellow| 122 | 20.167744  | 192.0.2.1    | 198.51.100.5 | HTTP     | HTTP/1.1 504 Gateway Time-out (text/html)     |
| red   | 123 | 20.490757  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 124 | 20.813770  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 125 | 21.136783  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 126 | 21.459796  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 127 | 21.782809  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 128 | 22.105822  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 129 | 22.428835  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 130 | 22.751848  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 131 | 23.074861  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 132 | 23.397874  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 133 | 23.720887  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 134 | 24.043900  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 135 | 24.366913  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 136 | 24.689926  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 137 | 25.012939  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 138 | 25.335952  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 139 | 25.658965  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |
| red   | 140 | 25.981978  | 203.0.113.0  | 192.0.2.1    | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...      |

## DETAILED ANALYSIS
### Part One: Identification of the Attack

**Type of Attack:**
The analysis of the given tcp/http log data from Wireshark indicates a **SYN Flood Attack**, a type of Denial of Service (DoS) attack.

**Understanding Network Attacks:**
Network attacks are malicious activities aimed at disrupting, damaging, or gaining unauthorized access to computer networks. They can range from simple intrusions to complex, coordinated attacks.

**Type of Attack Likely Resulting in the Symptoms:**
- **Denial of Service (DoS):** A DoS attack involves overwhelming a single target with a flood of traffic to make a service unavailable.
- **Distributed Denial of Service (DDoS):** A DDoS attack uses multiple systems to flood the target, making it even more difficult to mitigate.

**Difference Between DoS and DDoS:**
- **DoS:** Originates from a single source.
- **DDoS:** Originates from multiple sources, often using a botnet.

**Symptoms Observed:**
- The website is taking a long time to load and reporting a connection timeout error.
- These symptoms are typical of a DoS attack, where the server is overwhelmed by the volume of SYN packets.

### Part Two: Explanation of the Attack's Impact

**Description of the Attack:**
A SYN Flood Attack involves sending a large number of SYN requests to a target server, causing it to allocate resources for half-open connections and eventually exhaust its ability to handle legitimate connections.

**Symptoms or Characteristics:**
- **Large Volume of SYN Packets:** The log shows repeated SYN requests from the same source.
- **Incomplete Handshakes:** Many SYN requests without corresponding ACK responses.

**Log Example:**
- **13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: SYN**
- **13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP Destination Unreachable**

**Impact on the Organization's Network:**
- **Resource Exhaustion:** The server becomes overwhelmed and unable to process legitimate requests, leading to slow performance and timeouts.
- **Service Disruption:** The website becomes inaccessible to users, affecting the organization's online presence and functionality.

**Potential Consequences:**
- **Loss of Revenue:** If the website is commercial, downtime can lead to significant financial losses.
- **Customer Dissatisfaction:** Users may lose trust in the service's reliability.
- **Operational Impact:** Internal operations relying on the website may be disrupted.

**Securing the Network:**
- **Implement Rate Limiting:** Control the rate of incoming SYN packets.
- **SYN Cookies:** Use SYN cookies to manage TCP connections without consuming resources until a connection is fully established.
- **Firewall Rules:** Configure firewalls to detect and block SYN flood attacks.
- **DDoS Protection Services:** Employ services that specialize in mitigating DDoS attacks.

### Part Three: Detailed Elaboration

**Name of the Network Intrusion Attack:**
- **SYN Flood Attack**

**Description of the Attack's Impact on Network Performance:**
- **Resource Allocation:** Each SYN request causes the server to allocate resources for a potential connection.
- **Connection Table Overflow:** The server's connection table may overflow, leading to new connections being dropped.
- **Increased Latency:** Legitimate traffic experiences increased latency and connection timeouts.

**Example from Logs:**
- **13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: SYN**
- **13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: SYN**
- **13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: SYN**

These repeated SYN requests indicate the ongoing attack, causing resource exhaustion and resulting in the observed connection timeouts and slow website loading times.

### Conclusion

The logs point to a SYN Flood Attack, a type of DoS attack causing significant disruption to the network. By overwhelming the server with SYN requests, the attacker exhausts available resources, leading to connection timeouts and slow performance. Implementing rate limiting, SYN cookies, firewall rules, and DDoS protection can help mitigate such attacks and secure the network against future incidents.

## REPORT
### Analyze Network Attacks

### Section 1: Identify the Type of Attack That May Have Caused This Network Interruption

One potential explanation for the website’s connection timeout error message is a DoS attack. The logs show that the web server stops responding after it is overloaded with SYN packet requests. This event could be a type of DoS attack called SYN flooding.

### Section 2: Explain How the Attack is Causing the Website Malfunction

When the website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol. The handshake consists of three steps:

1. A SYN packet is sent from the source to the destination, requesting to connect.
2. The destination replies to the source with a SYN-ACK packet to accept the connection request. The destination will reserve resources for the source to connect.
3. A final ACK packet is sent from the source to the destination, acknowledging permission to connect.

In the case of a SYN flood attack, a malicious actor will send a large number of SYN packets all at once, which overwhelms the server’s available resources to reserve for the connection. When this happens, there are no server resources left for legitimate TCP connection requests.

The logs indicate that the web server has become overwhelmed and is unable to process the visitors’ SYN requests. The server is unable to open a new connection to new visitors who receive a connection timeout message.
