# 🛰️ **Exploring Routing Concepts**

Routers are **Layer 3 devices**. They operate at the **Network layer** of the Open Systems Interconnection (OSI) and the **Internet layer** of the Transmission Control Protocol/Internet Protocol (TCP/IP) networking models.

Routers are one of the most essential networking devices found within private and public networks. They allow network professionals to interconnect two or more different networks together and forward packets to their destinations.

For instance, routers can:
* **Interconnect different IP subnets**, allowing devices on one IP network to communicate with hosts on another IP network.
* **Interconnect networks with different media types**, such as connecting an Ethernet network with a fiber optic network.


## ⚙️ Core and Advanced Functions

Routers are built to perform many Layer 3 operations, such as:
* **Network Address Translation (NAT)**
* **Filtering traffic** using Access Control Lists (ACLs)
* **Virtual Private Network (VPN)** capabilities, allowing network professionals to set up site-to-site and remote access VPNs.

However, all routers have one **core function**: to route or forward packets to their destinations efficiently, using the **most suitable path**.

For instance, have you ever wondered how your computer or smartphone can communicate with servers on the internet? Or how routers can forward your packets to the intended destination network or host?

Routers are configured with **routing protocols**. These protocols use an **algorithm** that helps them determine the **best path** or route to a destination. Between your device and a server on the internet, many paths are available that can be used to forward the packets. However, not all paths are suitable due to various factors within each path.


## 🗺️ Finding the Best Path

Imagine if the routers within an Internet Service Provider (ISP) network forward packets along paths that were heavily congested with a lot of network traffic (load). All the internet subscribers of that particular ISP will experience **high latency**, which causes slow response times when they are communicating with hosts on the internet.

Using **dynamic routing protocols** helps routers calculate the best path from a source to a destination. They do this by assigning **metric values** to various factors about a path, such as the following:

* Cumulative bandwidth
* Latency
* Reliability
* Outgoing load (TX load)
* Receiving load (RX load)
* Hop count
* Path


## 📖 The Routing Table

Each algorithm within a dynamic routing protocol uses one or more of these factors to determine and install the best path to a destination within the **routing table** of a router.

Each router has a **local routing table** that contains a list of destination routes or paths. This table simply tells the router how to forward a packet to its destination.

# ➡️ **Packet Forwarding Example**

The following diagram shows a computer that wants to send a message to a remote device.

<div align="center">
  <img src="./images/01.png" width="600"/>

  Figure 9.1 – Network diagram
</div>

As shown in the preceding diagram, **PC 1** wants to send a message to **Router-B**, which has been configured with an IP address of `10.10.10.1`.

Before PC 1 places the message on the network media, it checks its **local routing table**. This is to determine whether the destination exists within the same network as PC 1 (the `192.168.1.0/24` network) or on a remote network.


## 💻 Step 1: PC 1 Checks its Routing Table

The following screenshot shows the routing table within PC 1.

<div align="center">
  <img src="./images/02.png" width="600"/>

  Figure 9.2 – PC 1 routing table
</div>

Since the destination `10.10.10.1` **does not exist** within its local `192.168.1.0/24` network, PC 1 sends the message to its **default gateway**. In this case, the default gateway is **Router-A** on the network.


## 🛰️ Step 2: Router-A Checks its Routing Table

When Router-A receives the message from PC 1, it inspects the **destination IP address** (`10.10.10.1`) within the Layer 3 header of the packet. It then checks its local routing table for a suitable route or path to forward the packet to its destination.

The following screenshot shows the routing table of Router-A.

<div align="center">
  <img src="./images/03.png" width="600"/>

Figure 9.3 – Routing table of a Cisco router
</div>

As shown in the preceding screenshot, the routing table contains a list of destination routes (paths) that are known to the router.

### Understanding the Routing Table

  * **Codes**: The code listed in the upper portion of the snippet indicates *how* a route was learned by the router.
  * **Routes**: In the lower portion of the snippet, there are various parent routes and child routes.
  * **Parent/Child Routes**: The child routes can be easily identified as they are indented compared to the parent routes (which are not indented).
  * **Route Codes (`C` and `L`)**: Each child route has a code that indicates how the route was learned.
      * **C**: This code indicates the route is **directly connected** to the router.
      * **L**: This code indicates it’s a **local route** that points to a specific IP address on the router itself.
  * **Route Information**: Each route contains a destination network followed by either the **exit interface** of the router or the **next hop address**.

> #### 📝 Important Note: Routing Logic
>
>   * A router will check its routing table using a **top-down approach** until it finds a suitable route.
>   * Once a suitable route is found, the router **stops searching** and forwards the packet to the destination based on the details specified within that route.
>   * A network route will specify the **exit interface** and/or the **next hop address**.
>       * **Exit Interface**: This simply indicates which port on the router should be used to forward the packet to its destination.
>       * **Next Hop Address**: This is the IP address of the next router to receive the packet along the way to the destination.


## 🏁 Step 3: Forwarding the Packet

Therefore, Router-A uses the following network route to forward the packet to Router-B:

```
C 10.10.10.0/30 is directly connected, GigabitEthernet0/0
```

Simply put, Router-A will forward the packet out from its **GigabitEthernet 0/0** interface, to which Router-B is connected.


## 🛑 Exception: No Route Found

However, if a default gateway or router does not have a valid route to a destination network, it will return a **Destination Unreachable** message to the sender.

# 🗺️ **Understanding Routing Protocols**

Routers can populate their routing tables with **directly connected routes**. These are networks that are physically attached to the local interfaces of the router.

However, a router is unable to determine the path or route to a destination network that is **not** directly connected. This includes remote networks on the internet or networks attached to other routers within an organization.

For instance, the following screenshot shows the routing table of Router-A, which has two directly connected routes/networks on the local router.

<div align="center">
  <img src="./images/04.png" width="600"/>

  Figure 9.4 – Routing table
</div>


As shown in the preceding diagram, Router-A contains:

  * The **10.10.10.0/30** network, which is directly connected to its `GigabitEthernet 0/0` interface.
  * The **192.168.1.0/24** network, which is directly connected to the `GigabitEthernet 0/1` interface.

The following diagram provides a visual representation of the routing table within Router-A.

<div align="center">
  <img src="./images/05.png" width="600"/>

Figure 9.5 – Network topology
</div>


## 🚧 The Problem of Remote Networks

However, what if the network topology were to expand to include additional networks that are interconnected with multiple routers? This can be seen in the following diagram.

<div align="center">
  <img src="./images/06.png" width="600"/>

Figure 9.6 – Network diagram
</div>

As shown in the preceding diagram, **Router-A** is **not** directly connected to the `10.20.20.0/24` and `172.16.1.0/24` networks.

Therefore, if **PC 1** wants to send a message to **PC 2** over the network, Router-A will **not be able to forward the message**. This is because those remote networks are not yet known to Router-A.

As a result, if PC 1 forwards a packet to Router-A with the destination IP address of `172.16.1.10`, Router-A will return a **Destination Host Unreachable** message to PC 1. This happens because a route to the destination host or network does not exist within the routing table of Router-A.

The following screenshot shows the routing table of Router-A on the new topology.

<div align="center">
  <img src="./images/07.png" width="600"/>

Figure 9.7 – Router-A routing table
</div>

As shown in the preceding screenshot, Router-A **does not have a network route** for the `172.16.1.0/24` network. Because of this, it will not be able to forward any packets to **PC 2**, which has an IP address of `172.16.1.10`.

The following screenshot shows the response from Router-A (PC 1's gateway), which indicates it does not have a valid route to the destination host.

<div align="center">
  <img src="./images/08.png" width="600"/>

Figure 9.8 – Destination unreachable message from the router
</div>


## 💡 The Solution: Dynamic Routing Protocols

A network professional can resolve this issue by configuring Router-A, Router-B, and Router-C with a **dynamic routing protocol**.

This type of protocol **automatically shares network routes between routers**. This allows them to update their routing tables with any network topology changes and ensures each router knows how to forward packets to its intended destination.

Many dynamic routing protocols are commonly implemented within organizations by network professionals. Each protocol has unique characteristics that define how they choose the most suitable path to a destination.

# ⚙️ **Dynamic Routing**

Dynamic routing protocols are designed to help routers automatically learn about destination networks by sharing routing information with other routers. The routing information that is shared between routers within an organization is used to add the **best suitable route** to a destination network within the routing table of each router.

Additionally, if a network or path is no longer available, the dynamic routing protocol automatically detects changes within the network topology. It shares updated routing information with all routers within the network to ensure their routing table is always up to date. Hence, if a router receives a packet with a destination IP address and the router no longer has an available route to the destination, the router informs the sender that the destination host or the network is unreachable.

> #### 📝 Important Note
>
> Each dynamic routing protocol is designed with an algorithm that calculates the **best suitable path** to a destination. It does this by determining the **metric** (or cost) of each available path and choosing the path with the **least metric** to install within the routing table.


### 🌟 Benefits of Dynamic Routing

Dynamic routing protocols provide the following benefits:

  * Automatically discover remote networks by sharing routing information between routers on a network.
  * Maintain an up-to-date routing table on all routers within the network.
  * Choose the best suitable destination path to forward packets to their destinations.
  * Can find a new best path in the event the current path is no longer available.


### Protocol Categories

The following diagram shows a breakdown of each dynamic routing protocol within the industry.

<div align="center">
  <img src="./images/09.png" width="600"/>

Figure 9.9 – Dynamic routing protocols
</div>

As shown in the preceding diagram, routing protocols belong to either **Interior Gateway Protocols (IGPs)** or **Exterior Gateway Protocols (EGPs)**.

  * **IGPs (Interior Gateway Protocols)**: These are dynamic routing protocols implemented *within* an organization's private network. They do not share routing information on the public internet. When all routers know about all networks within an organization, it is commonly referred to as a **converged network**.

> #### 📝 Important Note
>
> **Interior Gateway Routing Protocol (IGRP)** is a legacy Cisco proprietary routing protocol. It is no longer implemented on networks and has been replaced with its successor, **Enhanced Interior Gateway Routing Protocol (EIGRP)**.

Additionally, IGPs are further divided into two sub-categories:

1.  **Distance-Vector Protocols**

      * These protocols forward packets based on distance (a metric) and direction (the next hop).
      * Each distance-vector routing protocol uses an algorithm to calculate the best path and sends that information to its neighbor routers.
      * These protocols use factors relative to distance and direction, such as hop counts, bandwidth, reliability, outgoing and receiving load, and delays.
      * The algorithms within distance-vector routing protocols consist of the following:
          * A mechanism for exchanging routing information between neighbor routers.
          * **Distance-Vector routers send out their *entire routing table*** to immediate neighbor routers (this differs from Link-State, which only sends changes).
          * A mechanism for calculating the best path and adding the route(s) to the routing table.
          * A mechanism to detect and adapt to changes in the network topology and update the routing table.
      * **Examples:**
          * Routing Information Protocol (RIP)
          * Enhanced Interior Gateway Routing Protocol (EIGRP)

2.  **Link-State Protocols**

      * These protocols use the **cumulative bandwidth** to a destination network as the metric (referred to as "cost").
      * Each router configured with a link-state protocol builds its own **topological map** of the entire network. This map helps the router determine the shortest path to every destination.
      * Link-state routing protocols will only send an update to a neighbor router if there is a change within the network topology.
      * **Examples:**
          * Open Shortest Path First (OSPF)
          * Intermediate System - Intermediate System (IS-IS)

<!-- end list -->

  * **EGPs (Exterior Gateway Protocols)**: These are dynamic routing protocols implemented *between* different Autonomous Systems (ASs), such as ISPs, to share public network routes.
      * IGP routes *internal* to one AS, whereas EGP routes *between* ASs.
      * At the time of writing, the **Border Gateway Protocol (BGP)** is the only EGP that exists within the networking industry. It is used between ISPs to share their public networks with other ISPs on the internet.
      * BGP is a **path-vector** routing protocol that allows ISP routers to learn about other public networks and maintain an up-to-date routing table with BGP routes.


### 🚦 Administrative Distance

A router can be configured with multiple dynamic routing protocols to operate simultaneously. Each routing protocol operating on the router will use its algorithm to determine the best path to a destination network.

However, this raises a question: **which route should be added to the routing table?** A route to a single destination network can only appear once within the routing table. If a router is configured with both EIGRP and OSPF, and each protocol determines a "best path" to the same destination, the router must decide which route to use, since duplicates are not supported.

Usually, network professionals only configure one routing protocol within their organization. However, in situations where more than one is used, Cisco IOS routers use **Administrative Distance (AD)** to determine the **trustworthiness** of a route.

Each dynamic routing protocol is assigned a unique AD value. This value helps the router determine which route source is most trustworthy.

The following table shows the AD values for each route source for Cisco IOS routers.

<div align="center">
  <img src="./images/10.png" width="500"/>

Figure 9.10 – Administrative distance chart
</div>

As shown in the table, the router chooses the route source to a destination network that has the **lowest AD value**.

  * **Example**: If a router is configured with both EIGRP and OSPF, and each protocol finds a path to the same destination, the **EIGRP route will be added** to the routing table. This is because EIGRP has a default AD value of **90**, which is lower (more trustworthy) than OSPF's AD value of **110**.
  * **Exception**: If a network professional configures a **static route** to that same destination, the static route will be prioritized and added to the routing table, as its AD value is **1**.

Over the next few sub-sections, you will gain a solid foundation on various distance-vector, link-state, and path-vector routing protocols.


### ➡️ RIP (Routing Information Protocol)

RIP is a **legacy, distance-vector** routing protocol. It is no longer implemented on large enterprise networks due to its many limitations.

  * **Algorithm**: RIP uses the **Bellman-Ford algorithm**.
  * **Metric**: It uses **hop count** as the metric to calculate the best path. The hop count is simply the number of routers (hops) that exist on the path to the destination.
  * **Limit**: RIP uses a maximum hop count of **15**. A packet's hop count decrements by 1 at each router. If the hop count reaches 0, the last router discards the packet. This is similar to the Time To Live (TTL) value in an IP packet.
  * **Transport**: RIP uses **UDP port 520** to exchange messages between RIP-enabled routers.

The following diagram shows a network topology with routers configured using the RIP dynamic routing protocol.

<div align="center">
  <img src="./images/11.png" width="600"/>

Figure 9.11 – Routers using the RIP dynamic routing protocol
</div>

Let’s assume Router-A, Router-B, and Router-C are all managed by an organization and have been configured with RIP. The following screenshot shows the RIP routes that have been installed within the routing table of Router-A.

<div align="center">
  <img src="./images/12.png" width="600"/>

Figure 9.12 – Routing table
</div>

As shown in the preceding screenshot, there are three network routes (labeled 1, 2, and 3) that were discovered via RIP and added to Router-A's routing table.

#### Analyzing the First RIP Route

The first remote network route (`10.20.20.0/30`) is described as follows:

  * **`R`**: The `R` code indicates the network route was learned and added to the routing table via **RIP**.
  * **`10.20.20.0/30`**: This portion indicates the **destination network** by its network prefix.
  * **`[120/1]`**: This is the administrative distance and metric.
      * `120`: This value indicates the **Administrative Distance (AD)** for RIP. This shows the trustworthiness of the protocol.
      * `1`: This value represents the **metric** of the route. Since RIP uses hop count, we can determine that the destination network is **one hop away**.
  * **`10.10.10.1`**: This value is the **next-hop address**—that is, the IP of the next Layer 3 device (Router-B) that will receive the packet from Router-A.
  * **`00:00:15` (Timer)**: This time value increases as long as the route is installed in the routing table. It helps network professionals determine how long the router has known about this route.
  * **`GigabitEthernet0/0` (Exit Interface)**: This indicates the interface that Router-A will use to forward the packet toward its destination.

#### Disadvantages of RIP

While RIP seems good for automatically learning routes, it has many drawbacks:

  * RIP **broadcasts the *entire* routing table** of each router every **30 seconds**, regardless of whether a network change has occurred.
  * RIP does not support large networks with greater than **15 hops**.
  * **RIPv1** does not support networks that use custom subnet masks (VLSM).
  * **RIPv2** supports Variable Length Subnet Mask (VLSM) but doesn't allow manual specification of the custom subnet mask during configuration.

> #### 📝 Important Note
>
>   * **RIPng** is the next generation of RIP and supports **IPv6** routing.
>   * RIPv1 and RIPv2 support **IPv4** routing.
>   * RIPng uses **UDP port 521** to exchange messages.


### ➡️ OSPF (Open Shortest Path First)

Open Shortest Path First (OSPF) is a **link-state** dynamic routing protocol. It is commonly used within many organizations' networks, especially those with mixed-vendor devices (as it is an open standard).

  * **Algorithm**: OSPF uses the **Shortest Path First (SPF)** algorithm.
  * **Metric**: The SPF algorithm determines the cumulative bandwidth to a destination and chooses the path with the lowest **cost**. A low cost indicates a fast path, while a high cost indicates a slower link.
  * **Transport**: OSPF does not use TCP or UDP. It uses its own datagrams and is tagged in the IP protocol as **protocol number 89**.
  * **Adjacency**: Each OSPF-enabled router exchanges **Hello packets** with its neighbors to establish an *adjacency* (a mutual handshake).
  * **Updates**: Once the handshake is established, each router exchanges **Link-State Advertisements (LSAs)** of their directly connected networks. These LSAs contain information about the state and cost of each link.
  * **Database**: Once all OSPF-enabled routers collect the LSAs, they build the **Link-State Database (LSDB)**, also known as the topology table. This means every OSPF router knows the entire network topology.
  * **Routing**: After the LSDB is complete, the SPF algorithm is used to determine the best (shortest) path to all known networks and adds those paths to the routing table.

> #### 📝 Important Note
>
> OSPF-enabled routers send **Hello packets** to their neighbors every **10 seconds** by default to indicate their presence. A neighbor router is considered "down" or unavailable if a Hello packet is not received within **40 seconds**. If a neighbor router is down, all networks learned from that neighbor are removed from the routing table.

The following network topology shows routers configured with OSPF.

<div align="center">
  <img src="./images/13.png" width="600"/>

Figure 9.13 – OSPF network topology
</div>

As shown, Router-A, Router-B, and Router-C are configured to use OSPF to share routing information about their directly connected networks.

The following screenshot shows the routing table of Router-A.

<div align="center">
  <img src="./images/14.png" width="600"/>

Figure 9.14 – Router-A’s routing table
</div>

As shown in the screenshot:

  * The routing table contains directly connected routes (code `C`).
  * It also contains remote networks learned via OSPF (code `O`).
  * Notice that all standard OSPF routes (labeled 1 and 2) have the same AD value of **110**.
  * The third OSPF route (labeled 3), `O*E2`, indicates it is an **external route** (Type 2) that was redistributed into OSPF. Its purpose is to act as a default route (`0.0.0.0/0`) to the internet.

> #### 📝 Important Note
>
>   * **OSPFv2** is used on **IPv4** networks.
>   * **OSPFv3** is used on **IPv6** networks.


### ➡️ EIGRP (Enhanced Interior Gateway Routing Protocol)

EIGRP is a **hybrid, dynamic routing protocol**. It was a Cisco proprietary protocol until 2013, but organizations were long using OSPF as it is interoperable with mixed-vendor equipment.

  * **Algorithm**: EIGRP uses the **Diffusing Update Algorithm (DUAL)**.
  * **Metric**: DUAL uses the following factors as metrics to calculate the best path:
      * Bandwidth
      * Delay
      * Reliability
      * Outgoing load (TX load)
      * Receiving load (RX load)
      * By default, DUAL *only* uses **bandwidth and delay** to calculate the metric. The other metrics are disabled but can be enabled by a network professional.
  * **Transport**: EIGRP uses **protocol number 88**, encapsulated directly into IP datagrams, rather than TCP or UDP.
  * **Backup Path**: Unlike other protocols, EIGRP's DUAL calculates a **best path** (the Successor) and a **backup path** (the Feasible Successor) to the same destination. EIGRP ensures the backup path is loop-free and is ready to be placed in the routing table immediately if the primary route is no longer available.

The following network topology shows routers configured with EIGRP.

<div align="center">
  <img src="./images/15.png" width="600"/>

Figure 9.15 – EIGRP-enabled routers
</div>

Let’s assume Router-A, Router-B, and Router-C have all been configured with EIGRP. DUAL will calculate the metric (cost) to reach each network and install the paths within the routing tables.

The following screenshot shows the EIGRP network routes within the routing table of Router-A.

<div align="center">
  <img src="./images/16.png" width="600"/>

Figure 9.16 – Routing table
</div>

As shown in the screenshot:

  * The remote network routes (labeled 1, 2, and 3) are indicated by the `D` code, which stands for EIGRP.
  * Each of these internal routes has a default AD value of **90**.
  * The default route (`0.0.0.0/0`), labeled 3, has a code of `D*EX`. This indicates it is an **external EIGRP route** that was redistributed.
  * Notice its AD value is **170**. This is the default AD for external EIGRP routes, making them less trustworthy than internal EIGRP routes.


### ➡️ BGP (Border Gateway Protocol)

BGP is a **path-vector** routing protocol. It is the primary protocol used by ISPs to exchange routing information with each other over the internet.

  * **Transport**: BGP operates on **TCP port number 179**.
  * **Convergence**: Unlike IGPs, BGP is a **very slow converging** protocol. It does not send updates as soon as a topology change occurs. It was designed to be stable for massive, global-scale networks.
  * **Autonomous Systems (ASs)**: BGP was designed to operate *between* ASs. An AS is simply a large collection of public networks all managed by a single organization, such as an ISP. Each AS is assigned a unique **Autonomous System Number (ASN)**.

The following diagram shows different ASs (ISPs) interconnected using BGP to share their routing information.

<div align="center">
  <img src="./images/17.png" width="600"/>

Figure 9.17 – ASs
</div>

As shown, one ISP (AS) establishes an adjacency with another ISP using BGP to share routing information about their public networks. While they use IGPs (like OSPF or IS-IS) *inside* their own network, they use BGP to advertise their public networks to other ISPs around the world.

> #### 📝 Important Note
>
> When discussing BGP, it's important to know there are two versions:
>
>   * **External BGP (eBGP)**: Used between *different* ASs.
>   * **Internal BGP (iBGP)**: Used *within* a single AS.

The following screenshot shows the BGP routing table of a router.

<div align="center">
  <img src="./images/18.png" width="600"/>

Figure 9.18 – BGP routing table
</div>

As shown in the screenshot:

  * The destination networks are on the left.
  * The paths to those networks are on the right.
  * Since BGP is a **path-vector** protocol, the **`Path` column** shows the list of **AS numbers** a route has traversed. It does *not* show the number of hops. This AS path is the primary metric BGP uses to determine the best route and prevent loops.

> #### 💡 Tip
>
> If you are interested in seeing more BGP routing tables, check out the **BGP Looking Glass** project. This service is maintained by many ISPs around the world and allows limited, read-only access to their BGP routers. Simply type the Google search term `bgp looking glass` in your web browser.

---

# ➡️ **Static Routing**

**Static routing** allows network professionals to **manually configure** destination network routes within the routing table of a router.

Static routes always take precedence over any network route that was learned using a dynamic routing protocol. This is because static routes have a default **Administrative Distance (AD) of 1**, which is lower (and therefore more trustworthy) than the AD of any dynamic routing protocol. If you recall, the AD defines the trustworthiness of a route. Hence, if a network professional creates a static route to a destination network, the router will automatically trust this route over others.

-----

### ⚙️ Use Cases and Drawbacks

Network professionals can configure static routes on all routers within a small network. However, static routing has significant limitations:

  * **No Automatic Updates**: If the network topology changes, the static routes within the routers will **not automatically update** to reflect the changes. This is the primary difference compared to dynamic routing protocols.
  * **Manual Maintenance**: Static routes require a network professional to always update the configurations manually on *all* routers of an organization.
  * **Scalability**: Static routing is workable for small networks that change **infrequently** and where there are fewer IP networks.
  * **Misconfiguration Risk**: If a network professional misconfigures a static route on a router, the router will not forward packets correctly to the intended destination network. As a result, these misconfigurations can affect the performance of a network.
  * **"Black Hole" Routes**: A router will still forward packets to a network that is no longer reachable. This happens simply because the static route configured within the router tells the device how to forward packets and does not update the routing table if the network topology changes.
  * **Complexity**: Removing or modifying a static route requires the skills of a network professional. As an organization’s network grows, network professionals will need to implement a static route for each destination network on each router. Additionally, the complexity of troubleshooting issues increases as the network topology gets larger.

-----

### 🗂️ Types of Static Routes

The following are various types of static routes:

  * **Standard static route**: This type of static route specifies how to reach a specific destination network.
  * **Default static route**: A default static route is used when no other routes within the routing table of a router match the destination IP address of a packet. This type of route is usually configured to forward packets to the internet.
  * **Floating static route**: This type of static route functions as a **backup route** to a primary route on a router. It is configured with an AD that is *higher* than the primary route, so it is only used if the primary route is no longer available.
  * **Summary static route**: A summary static route is used to represent multiple destination IP networks in the form of a single, consolidated static route. Summary static routes are used to reduce the size of a routing table that has too many routes forwarding traffic to the same destination.

-----

### 🖥️ Static Routing Example

The following diagram shows a simple network topology where each router has been configured with static routing to forward traffic to remote networks.

<div align="center">
  <img src="./images/22.png" width="600"/>

  Figure 9.19 – Network topology
</div>

As shown in the preceding diagram, **Router-A** has to be configured with static routes to forward traffic to `10.20.20.0/30`, `172.16.1.0/24`, and the internet, as these networks are not directly connected to the router.

The following screenshot shows the static routes within the routing table of Router-A that are used to forward packets to the `10.20.20.0/30` and `172.16.1.0/24` networks.

<div align="center">
  <img src="./images/23.png" width="600"/>


  Figure 9.20 – Static routes
</div>


Lastly, the following screenshot highlights the **default static route**, which indicates the **gateway of last resort** on the routing table of Router-A.

<div align="center">
  <img src="./images/24.png" width="600"/>


  Figure 9.21 – Default static route
</div>

As shown in the preceding screenshot, the default static route (indicated by `S*`) is used when no other routes within the routing table of a router have a match for the destination IP address within a packet. Additionally, the next-hop address (`10.10.10.1`) of a default static route is used as the **gateway of last resort** on the router.

Having completed this section, you have learned about the fundamentals of static routing and dynamic routing.

---

# 📊 **Managing Bandwidth**

Within an organization’s network, many devices and users are sending and receiving messages to and from each other. Some users are uploading and downloading files from the internet, while others are having a teleconference meeting using a Voice over IP (VoIP) or Video over IP solution.

Overall, many different traffic types are traveling along a network.

  * Some of these traffic types use a connection-oriented protocol, such as **Transport Control Protocol (TCP)**.
  * Others use a connectionless protocol, such as **User Datagram Protocol (UDP)**.

## 🚦 TCP vs. UDP

One of the major differences between TCP and UDP is that **TCP provides guaranteed delivery** for packets over a network.

  * If a packet is not delivered to its intended destination, the sender will retransmit the message until the destination host provides an acknowledgment.
  * Packets that use TCP as their preferred transport layer protocol have a higher priority on the network because TCP provides guaranteed delivery.
  * Therefore, if a network becomes saturated or congested with too many packets, each device that wants to send a message tries to access the available bandwidth, which becomes an issue.

## 📥 Device Buffers

Furthermore, each networking device has two buffers for temporarily storing messages that are awaiting processing and forwarding. These are known as **port-based memory** and **shared memory**.

  * **Port Buffer (Port-based memory):** This buffer exists on each interface of a networking device.
      * It temporarily stores *inbound messages* that have to be processed by the device.
      * It also temporarily stores *outbound messages* that have already been processed and are waiting to be placed on the physical network.
  * **Shared Memory:** This is simply used to temporarily store all messages in a common buffer that is shared by all interfaces and the memory of the networking device.

If a networking device's buffer is filled, any additional messages will be **dropped** from the network.

  * If **TCP** messages are dropped, the sender will **retransmit** them to the destination.
  * However, if **UDP** messages are dropped, the sender will **not retransmit** them. This is because UDP does not have any mechanism to determine whether a packet arrived at a destination or not.

## 📞 The Problem with Time-Sensitive Traffic

For instance, voice and video traffic types use **UDP** as their preferred transport layer protocol. This is because UDP provides better capabilities for delivering messages that are time-sensitive over a network compared to TCP.

Imagine speaking to a colleague using a VoIP telephone within your office, and the dialog is not smooth.

  * Some packets are being sent and received more slowly than others (this is **jitter**).
  * Some packets are being dropped entirely.
  * This is happening because another employee is transferring a huge file and saturating the network.

## 💡 Solutions for Traffic Management

Network professionals use two types of solutions to ensure specific traffic types (like voice and video) have a high priority of accessing the bandwidth over others on a network:

1.  **Traffic Shaping**
2.  **Quality of Service (QoS)**

### 1\. Traffic Shaping

Traffic shaping allows network professionals to **create delays for some traffic types** using a traffic profile.

This technique is commonly used to improve latency and optimize the performance of a network, while also increasing the allocation of bandwidth for specific, important traffic types.

Simply put, if a sender is transmitting too many packets that are congesting the network, networking devices (such as switches) can create a delay or slow down the amount of traffic between that host and its destination. This allows other, higher-priority traffic types to access the bandwidth and flow with optimal speed, while the lower-priority traffic is delayed.

### 2\. Quality of Service (QoS)

QoS is another solution commonly implemented within many organizations’ networks. It helps control traffic on a network while ensuring the improved performance of mission-critical applications over a limited network capacity.

#### 📈 Key QoS Metrics

The following metrics are used within QoS to measure types of traffic over a network:

  * **Bandwidth:** The number of bits that can be transmitted in a second between a source and a destination.
  * **Congestion:** In a network, congestion results in packets being delayed while they are arriving at their destinations. Congestion occurs when there is a lot more traffic on the network than the available bandwidth can handle.
  * **Delay (Latency):** This measures the time a packet takes to travel between a source and a destination. Users on a congested network usually experience high latency (slow response time).
  * **Jitter:** This measures the **variation in the delay times** of incoming packets on a network. For instance, on an optimal network, all packets received from the same sender should have the same latency. Jitter increases on the network as users send and receive messages, saturating the network.
  * **Packet Loss:** This measures how many packets are discarded or dropped between a source and destination over a given time. Any discarded TCP messages are retransmitted, while UDP messages are not resent.

#### ⚙️ The QoS Prioritization Process

The following steps show how QoS prioritizes traffic on a network:

1.  **Classification:** Inbound traffic on a networking device is inspected. It is then placed within a waiting queue based on the **Differentiated Services (DS) field** of an IPv4 packet or the **Traffic Class field** of an IPv6 packet.
2.  **Marking:** This is the process where the QoS tools on the networking device modify one or more fields within the packet header to insert a priority value.
3.  **Queuing:** This phase is responsible for managing all the queues for outgoing messages on a networking device. Traffic is sent out of a networking device based on its priority.
4.  **Policing and Shaping:**
      * The **policing** feature is responsible for *discarding* or *dropping* packets that exceed a configured rate.
      * The **shaping** feature is responsible for *keeping* or *holding* the packets within a queue to delay them.
5.  **Congestion Avoidance:** This feature is used to proactively reduce the amount of congestion that exists within a network to reduce packet loss (for example, by dropping some packets *before* the buffer is completely full).

#### 🔬 The Classification Process in Detail

The following diagram shows the classification process when using QoS.

<div align="center">
  <img src="./images/25.png" width="700"/>

  Figure 9.22 – Classification process
</div>

As shown in the preceding diagram:

1.  **Traffic enters the router's interface.** A single flow of data arrives at the device.
2.  **A QoS tool is used to classify incoming traffic.** The router inspects the packet's header (e.g., the DS field) to identify what kind of traffic it is (e.g., voice, video, or file transfer).
3.  **Traffic is placed into a waiting queue with a priority.** Based on its classification, the packet is sorted into a high-priority, medium-priority, or low-priority queue.
4.  **Packets with a higher priority are transmitted before those with a lower priority.** The router's scheduler pulls packets from the high-priority queue first, ensuring that critical traffic (like VoIP) is sent out with the least amount of delay.

Having completed this section, you have gained an understanding of bandwidth management techniques such as traffic shaping and QoS.


---

# 🔄 **Delving into Switching Concepts**

As you have learned so far, network switches are designed and configured to forward frames to their destinations over a network. However, network switches have a lot of additional cool features that allow network professionals to enable special services and functions on a network.

In this section, you will learn how network professionals can:
* Distribute power over network cables to wireless access points and VoIP phones.
* Prevent a Layer 2 loop on a switching network.
* Aggregate multiple physical links into a single logical link between switches.
* Discover connected devices on a network.

## ⚡ Power over Ethernet (PoE)

**Power over Ethernet (PoE)** is the technology that allows **Direct Current (DC)** power to be sent over a copper Ethernet cable to devices. This reduces the need for a dedicated power supply and a separate Alternating Current (AC) power outlet for each device.

For instance, imagine you’re a network professional who has been assigned to install an access point in the center of a ceiling within a large office space.
* Before installing the access point, you notice that the closest AC power outlet is located in the furthest corner of the room.
* Additionally, attaching a power extension cord to the access point while running the power cord above the ceiling is perhaps not a good idea due to safety concerns.

Enabling the PoE feature on a **PoE-supported switch** will allow DC power to be distributed along the Ethernet cable to the access point. This hence reduces the need for a dedicated power supply and AC power outlet. The same concepts are commonly implemented to provide power to **VoIP phones** and **IP cameras** within organizations.

> #### 📝 Important Note
>
> Since an Ethernet cable is used to support both PoE and data, **PoE does not add any additional Ethernet capabilities** to the data that’s transported along the same cable.

### Standards and Specifications

PoE is defined by **IEEE 802.3af**, which was created in 2003. It specifies how electrical power can be delivered to another device by using:
* The **spare pairs** within a copper Twisted Pair cable (pins 4 and 5 or pins 7 and 8).
* The **data pairs** of an Ethernet cable (pins 1 and 2 or pins 3 and 6).

The concept of using PoE within networks allows organizations to save a lot of money by reducing the need for AC outlets and dedicated power supplies for devices.

* **PoE (IEEE 802.3af):** Provides up to **15.4 watts** of DC power with a maximum of **350 milliamps (mA)** of electrical current.
* **PoE+ (IEEE 802.3at):** An improved variation of PoE defined in 2009. It provides an increased power rating of up to **25.5 watts** with a maximum of **600 mA** of electrical current to devices.

> #### 📝 Important Note
>
> There are two modes of PoE:
> * **Mode A:** Delivers power on the **data pairs** (1, 2, 3, and 6).
> * **Mode B:** Delivers power on the **spare pairs** (4, 5, 7, and 8).

Therefore, before a network professional purchases PoE switches for their organization, it’s important to check the power rating of their PoE-supported devices (such as access points, IP cameras, and VoIP phones). This is to determine which version of PoE is more efficient to distribute power to these devices – that is, **PoE** or **PoE+**.

# 🌳 **Spanning-Tree Protocol** (STP)

When designing a network topology for any organization, it is essential to implement **redundancy** and **fault tolerance**. This ensures that multiple paths are available between a source and a destination.

While redundancy seems to be good, it is also very bad for Layer 2 switched networks. When multiple switches are interconnected to create redundancy, the design also creates a **Layer 2 loop**. Simply put, a Layer 2 loop exists whenever there are two or more available paths between a sender and the destination host on a switched network.

### 🏛️ The 3-Tier Architecture

The following diagram shows the 3-tier architecture that is commonly implemented within large organizations.

<div align="center">
  <img src="./images/26.png" width="600"/>

Figure 9.23 – 3-tier architecture model
</div>

As shown in the preceding diagram, this model allows for scalability and provides lots of redundancy between each layer:

  * **Access Layer**: Allows end devices to connect and access resources on the network.
  * **Distribution Layer**: Provides link aggregation, Quality of Service (QoS), and inter-VLAN routing.
  * **Core Layer**: This is the high-speed backbone of the network that interconnects the distribution layer, often between remote branch offices.

### ⚠️ The Problem: Layer 2 Loops

Let’s take a look at how a Layer 2 loop is formed when there are redundant paths within a switched network. The following diagrams show a small network with a redundant path between PC 1 and PC 3.

**Phase 1: Initial Frame**
As shown in the diagram, PC 1 sends a frame to PC 3. It inserts the MAC address of PC 3 (`CC:CC:CC:CC:CC:CC`) into the destination MAC address field of the frame header.

<div align="center">
  <img src="./images/27.png" width="600"/>

Figure 9.24 – Looping phase 1
</div>

**Phase 2: The Flood**
When the frame arrives on SW1, the switch inspects the destination MAC address. Let's assume SW1 does not know where PC 3 is. It forwards a copy of the frame out the two available paths: one via SW2 and one via SW3.

However, during this time, **PC 3 becomes unavailable** on the network. Because of this, SW3 no longer has the MAC address of PC 3 within its Content Addressable Memory (CAM) table.

<div align="center">
  <img src="./images/28.png" width="600"/>

Figure 9.25 – Looping phase 2
</div>

**Phase 3: The Loop Begins**
Since SW3 no longer has the MAC address of PC 3 in its CAM table, when SW3 receives the frame from SW1, it will **flood** the frame out of all other ports (except the one it arrived on). This means it sends the frame to SW2.

The same thing occurs when SW3 receives the frame *from* SW2. It floods that frame back to SW1. This is the default behavior of switches when a destination MAC address is not found in their CAM table.

<div align="center">
  <img src="./images/29.png" width="600"/>

Figure 9.26 – Looping phase 3
</div>

**Phase 4: The Broadcast Storm**
This loop will occur on all switches within the topology as long as each switch does not know how to find the destination host. For this reason, each switch will simply regenerate the frame and rebroadcast it over and over.

<div align="center">
  <img src="./images/30.png" width="600"/>

Figure 9.27 – Looping phase 4
</div>


The frames will loop in a never-ending cycle. This is because **Layer 2 frames do not contain a TTL (Time To Live) field** like Layer 3 packets do.

  * Packets contain TTL fields that are assigned a value (number). Each hop (router) along the way decreases the TTL value by 1. This ensures packets do not live forever on a network if a routing loop occurs. If the TTL value reaches 0, the router discards the packet.
  * Since frames do not have a TTL, they will not be automatically discarded. This creates a **broadcast storm** that can congest and crash an entire network.

### ⚠️ The Second Problem: Duplicate Messages

Another issue with redundant paths is the creation of duplicate messages between a source and a destination. To understand this, let's look at the following diagram, where PC 1 is sending a message to PC 3 (which is now connected).

**Phase 1: Initial Frame**
PC 1 sends a single frame to PC 3.

<div align="center">
  <img src="./images/31.png" width="600"/>

Figure 9.28 – Duplication phase 1
</div>

**Phase 2: Duplicate Delivery**
Without any loop prevention, when SW1 receives the frame, it will forward it to PC 3 using the two available paths (via SW2 and SW3). SW3 will then receive a copy from SW1 and another copy from SW2, and it will forward **both messages** to PC 3.

<div align="center">
  <img src="./images/32.png" width="600"/>

Figure 9.29 – Duplication phase 2
</div>

**Phase 3: Duplicate Replies**
Since PC 3 receives two copies of the message, it will **respond twice**. This duplication of responses will then multiply as it is sent back to PC 1, creating another storm.

<div align="center">
  <img src="./images/33.png" width="600"/>

Figure 9.30 – Duplication phase 3
</div>


## 💡 The Solution: Spanning-Tree Protocol (STP)

To resolve these issues, the **Spanning-Tree Protocol (STP)** was designed. STP is a **Layer 2 loop prevention protocol** that can detect any physical Layer 2 loops on a network and **logically block the redundant path**. This ensures only one active logical path between a source and destination is available at any time.

> #### 📝 Important Note
>
> STP is defined by the **IEEE 802.1D** standard.

The following diagram shows a network with STP enabled on all switches, which have already blocked a redundant path.

<div align="center">
  <img src="./images/34.png" width="600"/>

Figure 9.31 – STP enabled on all switches
</div>

As shown, when PC 1 wants to send a message to PC 3, there is only one active logical path, which prevents a loop.

However, if that primary path becomes unavailable, STP can detect the failure and automatically redirect the flow of traffic using one of the backup paths.

<div align="center">
  <img src="./images/35.png" width="600"/>

Figure 9.32 – Detecting a network failure
</div>
As shown, STP can detect a failure on an active path and automatically unblock a redundant path to redirect traffic.

### 📨 Bridge Protocol Data Units (BPDUs)

Whenever a switch is powered on, it sends **Bridge Protocol Data Unit (BPDU)** frames every 2 seconds to its neighbor switches. A BPDU contains the switch’s **Bridge ID**, which is made of:

  * Bridge Priority value
  * Extended System ID (Ext-ID)
  * MAC address

<div align="center">
  <img src="./images/36.png" width="600"/>

Figure 9.33 – BPDU frame
</div>

### 👑 The Root Bridge Election

The information in these BPDUs is used to elect a special switch as the **Root Bridge**.

1.  The Root Bridge informs all other switches to create one logical, loop-free path. It becomes the central reference point for all traffic.
2.  The switch with the **lowest bridge priority** gets elected as the Root Bridge.
3.  All Cisco switches have a default bridge priority of **32768**.
4.  If all switches have the same priority, the switch with the **lowest MAC address** will be elected as the Root Bridge.

Network professionals commonly configure their core or distribution layer switches to become the Root Bridge by manually lowering the bridge priority (in decrements of 4096).

Once the Root Bridge is elected, all other switches on the network create a logical path that points to the Root Bridge.

### 🗺️ STP Port Role Example

To get a better understanding of how STP identifies redundant paths, let’s look at the following network topology.

<div align="center">
  <img src="./images/37.png" width="600"/>

Figure 9.34 – Spanning-Tree network topology
</div>

As shown, each switch has a priority value (Priority + Ext-ID value) and a unique MAC address.

  * **SW1**: Priority 32769, MAC 000A.0011.1111
  * **SW2**: Priority **24577**, MAC 000A.0033.3333
  * **SW3**: Priority 32769, MAC 000A.0022.2222
  * **SW4**: Priority 32769, MAC 000A.0044.4444

#### Strategy for Identifying Port States

Here is a strategy for identifying the root bridge and port states on a network:

1.  **Identify the Root Bridge**: The central reference point for all traffic.
2.  **Identify Root Ports**: Ports *closest* to the Root Bridge (but not on the Root Bridge).
3.  **Identify Designated Ports**: Non-Root ports that are in a forwarding state.
4.  **Identify Alternate/Blocking Ports**: Ports that are logically blocked by STP to prevent a loop.

#### Step-by-Step Port Role Identification

You must follow these steps to identify the root bridge and port status on the topology:

1.  **Identify the Root Bridge**: **SW2** has the lowest priority value (**24577**), and therefore it becomes the **Root Bridge**.
2.  **Identify Root Ports (Easiest Paths)**: Next, the root ports are those with the most direct, lowest-cost path to the Root Bridge.
      * **SW1**'s port `Fa0/1` connects directly to the Root Bridge.
      * **SW4**'s port `Fa0/4` connects directly to the Root Bridge.
      * Therefore, **SW1 `Fa0/1`** and **SW4 `Fa0/4`** are **Root Ports (R)**.
3.  **Identify SW3's Root Port**: We need to determine the port role on SW3. There are two paths from SW3 to the Root Bridge:
      * Path 1: SW3 → SW1 → SW2
      * Path 2: SW3 → SW4 → SW2
      * Both paths have the same cost (interface bandwidth). We must observe the Bridge ID of the *next-hop* switch (SW1 vs. SW4). The path through the switch with the **lower Bridge ID** will be the preferred path.
      * SW1's Bridge ID (MAC `...1111`) is lower than SW4's (MAC `...4444`).
      * As a result, the path via SW1 is chosen, and **SW3 `Fa0/2`** becomes a **Root Port (R)**.
4.  **Identify Designated Port on SW1**: Since the preferred path from SW3 to the Root Bridge is via SW1, the other side of that link, **SW1 `Fa0/2`**, becomes a **Designated Port (D)**.
5.  **Identify Root Bridge Ports**: All ports on the Root Bridge are **Designated Ports (D)** by default. Therefore, SW2 `Fa0/1` and SW2 `Fa0/4` are Designated Ports.
6.  **Identify the Blocking Port**: Finally, the ports between SW3 and SW4 are yet to be assigned. One will be a Designated Port, and the other will be an Alternate/Blocking Port.
      * The switch with the **lower Bridge ID** will take precedence in having the Designated Port.
      * SW3's Bridge ID (MAC `...2222`) is lower than SW4's (MAC `...4444`).
      * Therefore, **SW3 `Fa0/3`** becomes a **Designated Port (D)**, and **SW4 `Fa0/3`** becomes the **Alternate/Blocking Port (A)**.

The following diagram shows the final port labels on each switch within the topology.

<div align="center">
  <img src="./images/38.png" width="600"/>

Figure 9.35 – STP port labels
</div>

---

# 🔗 **Port Aggregation** (EtherChannel)

**EtherChannel**, also known as **port aggregation**, is a technology that allows network professionals to **combine multiple physical links** into a **single logical connection** between switches. The primary purpose is to aggregate (or sum up) the bandwidth between these devices.

### 🚧 The Problem: Redundancy vs. Aggregation

If a network professional connects two network cables to the Gigabit Ethernet interfaces of two switches, their goal might be to double the bandwidth.

However, **Spanning-Tree Protocol (STP)** will identify this as a redundant path. To prevent a Layer 2 loop, STP will **logically block one of the links**, leaving only one link active for transmitting messages.

The following diagram illustrates this exact problem.

<div align="center">
  <img src="./images/39.png" width="600"/>


  Figure 9.36 – STP blocking a redundant path
</div>

As shown in the diagram, the objective was to combine the bandwidth of both Gigabit Ethernet interfaces to create a sum of 2 Gigabits per second (Gbps) between SW1 and SW2. However, because this creates redundant links, STP blocks one of them, completely defeating the goal of aggregation.

### 💡 The Solution: EtherChannel

To solve this issue, you can use **EtherChannel**. This technology allows a network professional to successfully aggregate the bandwidth of two or more physical connections, creating a single logical link. This logical link supports much greater bandwidth between devices.

Key benefits of using EtherChannel include:

  * **Hardware Re-use**: The existing switch interfaces are used to create the EtherChannel link, so network professionals do not need to upgrade the hardware components of a switch that already supports the technology.
  * **Load Balancing**: EtherChannels create load balancing of network traffic between the bundled links on a network.
  * **Redundancy**: The technology also helps with traffic aggregation while providing redundancy (if one physical link in the bundle fails, traffic automatically redirects to the remaining links).

### 🤝 LACP (Link Aggregation Control Protocol)

The **Link Aggregation Control Protocol (LACP)** is an open-source protocol defined by **IEEE 802.3ad**. It allows switches from any vendor to form EtherChannels with each other.

An LACP EtherChannel is formed when two switches use compatible modes on their interfaces. The **Active** LACP mode, for example, actively tries to negotiate an EtherChannel.

The following table shows the results of different LACP mode combinations on SW1 and SW2.

<div align="center">
  <img src="./images/40.png" width="600"/>

  Figure 9.37 – LACP modes
</div>

### 📋 Requirements for EtherChannel

For an EtherChannel to be established successfully between switches, several requirements must be met on all participating interfaces:

  * The same **type of interface** must be used (e.g., all GigabitEthernet).
  * The same **number of interfaces** must be used in the bundle.
  * The **speed and duplex** settings must be the same on all interfaces.
  * The same **configurations** (such as allowed VLANs and Native VLAN) must be applied to all interfaces.

The following diagram shows an example of an EtherChannel that is **unable to form**. This is because there is a **duplex mismatch** (SW1 is set to Half, SW2 is set to Full).

<div align="center">
  <img src="./images/41.png" width="600"/>

  Figure 9.38 – Unable to form an EtherChannel
</div>

When the configurations are the same on all interfaces being used, the EtherChannel is established successfully.

<div align="center">
  <img src="./images/42.png" width="600"/>

  Figure 9.39 – Establishing an EtherChannel
</div>

If one of the physical interfaces of an EtherChannel becomes unavailable or has any misconfigurations, the **entire EtherChannel is broken**. All the physical interfaces will then function independently from each other (which will likely cause STP to block one of them again).

---