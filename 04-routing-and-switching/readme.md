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