
# Deep Network Model Evaluation Prompts

---

## 1. OSPF Route Summarization
**Prompt:**  
Explain how OSPF route summarization can reduce routing table size and improve performance in a multi-site enterprise network. Include example configurations.

- **Blueprint Topic:** CCNP ENCOR 350-401 – *Layer 3 Technologies: OSPF*
- **Use Case:** Simplifying routing across remote branches and data centers.

**Answer:**  

OSPF route summarization helps reduce the size of routing tables and improves network performance by limiting the amount of routing information exchanged between routers. This is especially useful in multi-site networks.

Reduced Routing Table Size: Summarization reduces the number of routes each router needs to store.
Improved Performance: Less routing information translates to faster convergence and reduced CPU/memory usage.
Simplified Configuration: Easier management of routing information across the network.
Example Configuration (on a border router):

Cisco Configuration

```config
router ospf 1
 area 0.0.0.0
 auto-summary
 summary-address 192.168.0.0 255.255.0.0
```
This configuration summarizes routes for the 192.168.0.0/16 network into a single advertisement. This reduces the routing table size on neighboring routers.


---

## 2. Netmiko Interface Status Script
**Prompt:**  
Generate a Python script using Netmiko to pull interface status from a list of Cisco IOS devices and save the output to a CSV file.

- **Blueprint Topic:** CCNP ENAUTO 300-435 – *Python and Automation Tools*
- **Use Case:** Routine automation of interface checks across multiple devices.

**Answer:**  

Does not compute 💀



---

## 3. EEM-Based Interface Auto-Shutdown
**Prompt:**  
How would you use EEM (Embedded Event Manager) to automatically shut down an interface after detecting a specific syslog event on a Cisco switch?

- **Blueprint Topic:** CCNP ENCOR 350-401 – *Infrastructure Services: Network Management*
- **Use Case:** Reactive mitigation of interface flapping or rogue device events.

**Answer:**  

To use EEM to automatically shut down an interface upon detecting a specific syslog event, follow these steps:

Define the Event: Identify the syslog event you want to monitor.
Create EEM Policy: Use the event manager applet command to create a policy.
Configure the Trigger: Specify the syslog event that will trigger the policy.
Add the Action: Include the shutdown command for the interface.
Here's a sample configuration:

```text
event manager applet syslog-shutdown
 event syslog pattern Specific Syslog Message
 action 1.0 shutdown interface GigabitEthernet0/1
This policy will shut down GigabitEthernet0/1 when the specified syslog message is detected.
```

---

## 4. Secure Network Design with 802.1X
**Prompt:**  
Design a secure wired and wireless network for a healthcare provider using VLANs, 802.1X, and identity-based policies. Include a high-level diagram and explanation.

- **Blueprint Topics:**  
  - CCNA 200-301 – *Security Fundamentals*  
  - CCNP ENCOR 350-401 – *Security: NAC and 802.1X*
- **Use Case:** Enforcing identity-driven access in sensitive environments.

**Answer:**  

Secure Network Design for Healthcare Provider
Goal: To design a secure network accommodating diverse access needs while complying with HIPAA regulations.

I. High-Level Diagram

```text
+-------------------+      +-------------------+      +-------------------+
|    Internet       |------|       Firewall      |------|  Core Switch      |
+-------------------+      +-------------------+      +-------------------+
                                                         |
                                                         | VLANs + 802.1X
                                                         |
    +-------------------+  +-------------------+  +-------------------+
    |  Guest Wireless   |  | Medical Devices   |  |  Staff Wireless   |
    |   (Isolated VLAN) |  |    (Secure VLAN)  |  |   (Secure VLAN)   |
    +-------------------+  +-------------------+  +-------------------+
              |                          |                          |
              |                          |                          |
    +-------------------+  +-------------------+  +-------------------+
    |  Wired Admin PCs |  |  Wired Lab Equip |  |   Wired Staff PCs |
    |   (Secure VLAN)   |  |   (Secure VLAN)   |  |   (Secure VLAN)   |
    +-------------------+  +-------------------+  +-------------------+
```
II. Network Components

Firewall: Acts as the perimeter defense, protecting the internal network from external threats.
Core Switch: Supports VLANs, 802.1X, and is the central point for network traffic.
Access Switches: Distribute network access to various devices.
Wireless Access Points (WAPs): Provide wireless connectivity.
III. VLAN Segmentation

VLAN 10: Medical Devices: Highly secure VLAN for critical medical equipment. Access restricted to authorized staff.
VLAN 20: Staff Wireless: Secure VLAN for staff devices requiring network access.
VLAN 30: Wired Staff PCs: For administrative and operational PCs.
VLAN 40: Guest Wireless: Isolated VLAN with limited access for guest users. No access to internal resources.
VLAN 50: Wired Lab Equipment: Secure VLAN for lab equipment with specific access control.
IV. Security Measures

802.1X Authentication: Implemented on all wired and wireless networks requiring access to sensitive data. Users/devices are authenticated before granted network access.
Identity-Based Policies: Network access based on user/device identity. Different access levels and privileges assigned according to roles.
ACLs (Access Control Lists): Applied to VLANs to restrict traffic flow and prevent unauthorized access.
Encryption: Wireless networks secured with WPA3 encryption.
Regular Security Audits: Periodic reviews to ensure network security posture.
V. Explanation

Network Segmentation: VLANs separate different types of traffic, minimizing the impact of security breaches.
Secure Access: 802.1X ensures only authorized users/devices can access the network.
Compliance: The design supports HIPAA compliance by protecting sensitive patient information.
Flexibility: Allows for easy addition/removal of devices and users.
VI. Key Considerations

Scalability: Design should accommodate future growth.
Redundancy: Implement redundant links for high availability.
Monitoring: Continuous monitoring for security threats.
This design provides a robust and secure network infrastructure for a healthcare provider, ensuring compliance and protecting sensitive data.

---

## 5. ACL Behavior and Design Choices
**Prompt:**  
Compare the behavior of standard ACLs vs. extended ACLs when placed inbound vs. outbound on Cisco routers. When would you choose one over the other in a DMZ design?

- **Blueprint Topic:** CCNA 200-301 – *IP Services: ACLs*
- **Use Case:** Designing access control in edge routers and DMZs.

**Answer:**  
Standard vs. Extended ACLs on Cisco Routers
Here's a comparison of standard and extended ACLs, considering their placement (inbound/outbound) and suitability for a DMZ design:

I. Standard ACLs

Filtering Criteria: Filter based solely on source IP address.
Inbound Placement: Blocks traffic originating from specific source IP addresses before it reaches the router. Useful for basic filtering based on source.
Outbound Placement: Blocks traffic destined for specific source IP addresses. Less common as it doesn’t address destination-specific needs.
Limitations: Limited filtering capability; doesn't consider destination IP, protocols, or ports.
II. Extended ACLs

Filtering Criteria: Filter based on source and destination IP addresses, protocols, and port numbers.
Inbound Placement: Offers granular control by allowing filtering based on specific traffic patterns, protocols, and port numbers directed towards the router.
Outbound Placement: Similarly provides detailed control over traffic leaving the router, allowing filtering based on destination IPs, ports, etc.
Advantages: More versatile and allows for precise traffic management.
III. DMZ Design Considerations

Standard ACLs in DMZ: Typically not recommended. They lack the granularity needed for a secure DMZ where specific services (e.g., web, mail) need controlled access.
Extended ACLs in DMZ: Highly recommended.
Inbound: Control which external traffic can reach DMZ servers based on source IP, protocol, and port. Allow only necessary traffic (e.g., HTTP/HTTPS to a web server).
Outbound: Control what traffic DMZ servers can send to the internal network. Deny unnecessary access to protect internal resources.
Specific Scenarios:
For a web server in the DMZ, use extended ACLs to permit inbound HTTP/HTTPS traffic from any source and deny all other traffic.
Use extended ACLs to restrict outbound access from the DMZ to specific internal resources, preventing unauthorized access.
IV. Summary Table

Feature	Standard ACLs	Extended ACLs
Filtering Criteria	Source IP	Source/Destination IP, Protocol, Port
Inbound Use	Basic source filtering	Granular traffic control
Outbound Use	Limited	Comprehensive traffic control
DMZ Suitability	Low	High
Conclusion: Extended ACLs are essential for DMZ designs due to their ability to implement fine-grained security policies and protect both DMZ servers and internal networks. Standard ACLs lack the necessary precision for this purpose.

---

## 6. YANG + RESTCONF for Interface Config
**Prompt:**  
Write a YANG model snippet that defines an interface configuration with speed, duplex, and description. Then, show how to use RESTCONF to push this to a device.

- **Blueprint Topic:** CCIE Enterprise Infrastructure v1.1 – *Automation: YANG, NETCONF/RESTCONF*
- **Use Case:** API-driven configuration management for network consistency.

**Answer:**  
Does not compute 💀

---

## 7. SNMPv2 vs. SNMPv3 Migration
**Prompt:**  
What’s the difference between SNMPv2 and SNMPv3 in terms of security? How would you migrate a large network from v2 to v3 with minimal disruption?

- **Blueprint Topic:** CCNP ENCOR 350-401 – *Infrastructure Services: SNMP*
- **Use Case:** Improving observability while maintaining compliance.

**Answer:**  

SNMPv2 vs. SNMPv3 Security
SNMPv3 significantly enhances security over SNMPv2:

SNMPv2: Uses community strings for authentication, which are sent in cleartext, making it vulnerable to eavesdropping and unauthorized access. No encryption is provided.
SNMPv3: Introduces authentication using HMAC-MD5 or HMAC-SHA, encryption using DES or AES, and improved access control via Views. This protects against unauthorized access, eavesdropping, and modification of management data.
Migration Strategy from SNMPv2 to v3
Migrating a large network from SNMPv2 to v3 with minimal disruption involves a phased approach:

Pilot Deployment: Start with a small segment of the network to test compatibility and identify potential issues.
Dual Stack Configuration: Configure devices to support both SNMPv2 and v3 simultaneously. This allows gradual transition without immediate disruption.
Authentication Setup: Enable authentication on SNMPv3, ensuring only authorized devices can communicate.
Encryption Enablement: Implement encryption to protect data in transit.
View Configuration: Define Views to restrict access to specific parts of the MIB (Management Information Base).
Monitoring and Validation: Continuously monitor the network for any issues and validate that SNMPv3 is functioning correctly.
Phase-Out v2: Once SNMPv3 is fully validated, gradually disable SNMPv2 on devices and the NMS (Network Management System).
Documentation: Maintain thorough documentation throughout the process.
This phased approach minimizes downtime and ensures a smooth transition to the more secure SNMPv3 protocol.

---

## 8. IPSLA WAN Monitoring & Scripting
**Prompt:**  
Simulate an SLA monitor using Cisco IPSLA to detect WAN latency. Provide CLI configuration and describe how a script could react to a threshold breach.

- **Blueprint Topic:** CCNP ENCOR 350-401 – *Infrastructure Monitoring: IP SLA*
- **Use Case:** Real-time latency detection for VoIP/critical apps.

**Answer:**  

Does not compute 💀

---

## 9. VXLAN vs. VLAN in DC Fabrics
**Prompt:**  
Explain the key differences between VXLAN and traditional VLANs in a data center fabric. When would you recommend using VXLAN with EVPN?

- **Blueprint Topic:** CCIE Enterprise Infrastructure – *Network Virtualization: VXLAN, EVPN*
- **Use Case:** Multi-tenant DC networking with extended Layer 2 segments.

**Answer:**  
VXLAN vs. Traditional VLANs
Here's a breakdown of the key differences between VXLAN and traditional VLANs in a data center fabric:

#### Traditional VLANs:

**Layer 2 Technology:** Operate within a single Layer 2 broadcast domain.
**Limited Scalability:** Restricted to 4094 VLANs, limiting the number of networks that can be supported.
**Spanning Tree Protocol (STP):** Used to prevent loops, which can cause network instability and inefficiencies.
Limited Mobility: Difficult to extend VLANs across multiple data centers.

####VXLAN (Virtual Extensible LAN):

**Layer 2 over Layer 3:** Encapsulates Layer 2 Ethernet frames within Layer 3 UDP packets, enabling traffic to traverse Layer 3 networks.
**Scalability:** Supports up to 16 million logical networks, significantly increasing scalability compared to VLANs.
Eliminates STP: By operating over Layer 3, VXLAN eliminates the need for STP, improving network performance.
Enhanced Mobility: Enables seamless Layer 2 extension across geographically dispersed data centers.
When to Recommend VXLAN with EVPN
VXLAN with EVPN (Ethernet VPN) is recommended in the following scenarios:

**Large-Scale Data Centers:** When you require support for a vast number of logical networks beyond the limitations of VLANs.
Multi-Tenant Environments: For providing isolated networks to different tenants without VLAN limitations.
**Dynamic Workload Mobility:** To enable virtual machine (VM) mobility across data centers without changing IP addresses.
Active-Active Data Centers: To create a unified fabric that allows for workload balancing and disaster recovery.
Simplified Network Management: EVPN provides a control plane for VXLAN, automating network configuration and simplifying management.
EVPN improves VXLAN by providing a more efficient control plane, reducing flooding and improving MAC address learning. This makes VXLAN with EVPN ideal for modern, scalable, and dynamic data center environments.

---

## 10. pyATS BGP Validation
**Prompt:**  
show me how to verify BGP neighbor status and log mismatches against an expected state YAML file.


- **Blueprint Topic:** CCNP ENAUTO 300-435 – *Automated Testing and Validation: pyATS*
- **Use Case:** CI/CD-style post-deployment BGP validation.

**Answer:**  
here's a solution combining BGP neighbor status verification with log mismatch detection using a YAML configuration file and Python scripting. This approach provides automation and clarity.

YAML Configuration File (bgp_config.yaml):
yaml

```bash
neighbors:
  - peer_ip: 192.168.1.1
    expected_state: Established
    expected_messages:
      - BGP neighbor 192.168.1.1 is Established
  - peer_ip: 192.168.1.2
    expected_state: Idle
    expected_messages:
      - BGP neighbor 192.168.1.2 is Idle
      - BGP peer 192.168.1.2 is in state Idle
```
Python Script (verify_bgp.py):

```python
import yaml
import subprocess

def verify_bgp_neighbors(config_file):
    with open(config_file, 'r') as f:
        config = yaml.safe_load(f)

    for neighbor in config['neighbors']:
        peer_ip = neighbor['peer_ip']
        expected_state = neighbor['expected_state']
        expected_messages = neighbor['expected_messages']

        # Execute show bgp summary command
        command = ['show', 'bgp', 'summary']
        try:
            output = subprocess.check_output(command, text=True, stderr=subprocess.STDOUT)
        except subprocess.CalledProcessError as e:
            print(fError executing command: {e}
            continue

        # Check BGP neighbor state
        state_found = False
        for message in expected_messages:
            if message in output:
                state_found = True
                break

        if not state_found:
            print(fMismatch: BGP neighbor {peer_ip} is not in expected state '{expected_state}'. Found messages are:
            for line in output.splitlines():
                print(line)

if __name__ == main__
    verify_bgp_neighbors('bgp_config.yaml')
```
**Explanation**:

**YAML Configuration:** The bgp_config.yaml file defines expected states and messages for each BGP neighbor.
Python Script:
Loads the YAML configuration file.
Iterates through each configured neighbor.
Executes the show bgp summary command using subprocess.
Compares the command output against expected messages.
Prints mismatch details if the actual state doesn't match the expectation.
Error Handling: Includes error handling for command execution failures.
How to Run:

Save the YAML configuration as bgp_config.yaml.
Save the Python script as verify_bgp.py.
Execute the script from a terminal with access to the Cisco device: python verify_bgp.py.

**Important Notes:**

**Access:** Ensure the script is run with credentials that have permissions to execute show commands on the Cisco device.
Adaptation: Adjust the show bgp summary command and expected message patterns based on the specific Cisco device and IOS version.
Logging: Consider adding logging to a file for historical analysis.
Security: Be cautious about storing credentials directly in the script. Use environment variables or secure configuration management for production use.


---
