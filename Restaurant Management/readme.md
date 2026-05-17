# Modern Hotel Network: Full-Stack Infrastructure Design & Implementation

This project is a comprehensive networking solution for a three-story modern hotel. It implements a hierarchical network design featuring departmental VLAN segmentation, dynamic routing with OSPF, secure remote management via SSH, and hardened Layer 2 port security.

## 🏨 Project Overview & Requirements
The goal of this project was to design a network where three distinct floors communicate via a central server room. 

### Core Specifications:
* **Inter-Router Links:** Serial DCE cables connecting three 2911 routers.
* **Network Backbone:** `10.10.10.0/30`, `10.10.10.4/30`, `10.10.10.8/30`.
* **Routing Protocol:** OSPF (Open Shortest Path First) for global reachability.
* **Departmental VLANs:** 8 distinct VLANs across 3 floors (VLAN 10 through 80).
* **IP Management:** Router-based DHCP server for all departments.
* **Security:** SSH for remote login and Sticky MAC Port Security in the IT Dept.

---

## 🗺️ Master Network Topology
![Full Hotel Architecture](./hotel_media/topology_main.png)
*Figure 1: Complete architecture featuring three routers, departmental switches, and integrated wireless access points.*

---

## 🛠️ Step-by-Step Configuration & Evidence

Below is the complete documentation of every configuration phase. Click each section to view the technical implementation and screenshots.

<details>
<summary><b>Phase 1: Basic Router Connectivity & Interface Setup</b></summary>

The routers are the heart of the system, connected via Serial DCE cables. All interfaces were manually enabled and assigned IPs based on the 10.10.10.x/30 backbone.

![Serial Interface Config](./hotel_media/serial_config.png)
<br>
![Interface Status Brief](./hotel_media/int_brief.png)
<br>
*Verification: CLI output showing Gigabit and Serial interfaces in an 'up/up' state.*
</details>

<details>
<summary><b>Phase 2: VLAN Design & Inter-VLAN Routing</b></summary>

To meet the requirement of 8 departments, I used "Router-on-a-Stick." Each department (Reception, Finance, IT, etc.) was assigned a specific VLAN ID and sub-interface.

![VLAN Sub-interface Configuration](./hotel_media/vlan_sub_int.png)
![VLAN Table Verification](./hotel_media/vlan_brief.png)
*Details: Encapsulation dot1Q was applied to each sub-interface to map VLAN IDs to their respective network gateways.*
</details>

<details>
<summary><b>Phase 3: Dynamic IP Assignment (DHCP)</b></summary>

I configured DHCP pools on each router so that every laptop, PC, and smartphone receives an IP automatically.

![DHCP Pool Config](./hotel_media/dhcp_config.png)
![Client IP Verification](./hotel_media/dhcp_client_success.png)
*Action: Verification of a PC successfully obtaining an IP, Subnet Mask, and Gateway from the router pool.*
</details>

<details>
<summary><b>Phase 4: OSPF Dynamic Routing Protocol</b></summary>

OSPF was configured on all three routers to advertise departmental networks. This ensures that a PC on the 1st floor can find the shortest path to a server on the 3rd floor.

![OSPF Configuration](./hotel_media/ospf_config.png)
![Routing Table OSPF Routes](./hotel_media/routing_table.png)
*Result: The routing table now shows 'O' (OSPF) learned routes for all remote departmental subnets.*
</details>

<details>
<summary><b>Phase 5: Wireless Infrastructure (Laptops & Mobile)</b></summary>

Each floor features high-speed Wi-Fi. Access points were configured with unique SSIDs and WPA2-PSK encryption.

![Access Point Security](./hotel_media/ap_security.png)
![Smartphone Wireless Setup](./hotel_media/mobile_config.png)
![Laptop Connection Screen](./hotel_media/laptop_wifi_connect.png)
*Process: Manually entering the SSID and WPA2-PSK password on smartphones and tablets to establish connectivity.*
</details>

<details>
<summary><b>Phase 6: Secure Remote Management (SSH)</b></summary>

Remote access is secured via SSH using the username `itech` and password `itech`. This allows IT staff to manage routers from any floor.

![SSH Configuration](./hotel_media/ssh_setup.png)
![Successful SSH Remote Session](./hotel_media/ssh_login_success.png)
*Evidence: Command prompt showing a successful remote login to the FLOR2 Router from a Test-PC.*
</details>

<details>
<summary><b>Phase 7: IT Department Port Security</b></summary>

To prevent unauthorized devices from plugging into the IT network, Port Security was enabled on `fa0/1`.
* **Mode:** Sticky (learns the MAC automatically).
* **Violation:** Shutdown (disables the port if an intruder connects).

![Port Security Configuration](./hotel_media/port_sec_config.png)
![Port Security Verification Status](./hotel_media/port_sec_status.png)
![Sticky MAC Learning Evidence](./hotel_media/sticky_mac_verified.png)
*Verification: Using 'do show port-security' to confirm the Test-PC is the only allowed device.*
</details>

<details>
<summary><b>Phase 8: Running Configuration & Startup</b></summary>

The final `show running-config` confirms that all protocols (OSPF, SSH, Port-Security) are saved and active.

![Running Config Part 1](./hotel_media/run_config_1.png)
![Running Config Part 2](./hotel_media/run_config_2.png)
*Summary: Comprehensive view of the startup-config settings.*
</details>

---

## 🧪 Testing & Connectivity Results

### Departmental Reachability
I performed pings between the 1st Floor (Reception) and the 3rd Floor (IT) to verify that OSPF and Inter-VLAN routing are working perfectly.

![Cross-Floor Ping Result](./hotel_media/ping_test_results.png)
*Status: 0% Packet Loss – Success!*

---

## 🎥 Video Demonstration
The following video provides a complete walkthrough of the network, showing real-time pings, the SSH login process, and wireless device connections.

[Click to Watch the Full Hotel Network Walkthrough](./hotel_media/demo_video.mp4)

---

## 📝 Project Identity
* **Lead Engineer:** Sneha
* **Location:** Kalburgi
* **Project Date:** May 2026
* **Environment:** Cisco Packet Tracer 8.x
