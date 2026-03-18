<p align="center">
  <img src="https://raw.githubusercontent.com/ayogun/42-project-badges/main/covers/cover-net_practice.png" alt="NetPractice cover" width="100%">
</p>

<h1 align="center">
  <a href="https://github.com/fernandoruanb/net_practice">
    <img src="https://raw.githubusercontent.com/ayogun/42-project-badges/main/badges/netpracticee.png" width="200" alt="Netpractice Badge"\>
  </a>
  <br>
  NetPractice
  <br>
</h1>

<h4 align="center">
  An introductory networking project focused on IPv4, subnet masks, routing, and basic communication logic through interactive exercises in a web interface.
</h4>

<p align="center">
  <img src="https://img.shields.io/badge/Final%20Score-100%2F100-00C853?style=for-the-badge" alt="Final Score 100/100">
  <img src="https://img.shields.io/badge/Topic-Networking-00599C?style=for-the-badge" alt="Networking">
  <img src="https://img.shields.io/badge/Protocol-IPv4-blueviolet?style=for-the-badge" alt="IPv4">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" alt="Status Completed">
</p>

<p align="center">
  <a href="#about-the-project">About</a> •
  <a href="#core-idea">Core Idea</a> •
  <a href="#training-and-evaluation">Training & Evaluation</a> •
  <a href="#ipv4-and-subnet-masks">IPv4 & Subnet Masks</a> •
  <a href="#switches-routers-and-the-internet">Switches, Routers & Internet</a> •
  <a href="#practical-examples">Practical Examples</a> •
  <a href="#how-to-use">How To Use</a> •
  <a href="#team">Team</a>
</p>

---

## About the Project

**NetPractice** is an introduction to the basic logic of **computer networks** for 42 cadets.

It is not meant to reach the full depth of a certification like **CCNA**, but it builds a solid foundation for understanding how machines communicate, how IPv4 addressing works, how subnet masks divide networks, and how routing begins to make sense in practice.

What makes this project interesting is that it teaches networking in a very direct way:

- by observation
- by reasoning
- by fixing broken configurations
- by understanding why two devices can or cannot talk to each other

Instead of writing code, the project trains the ability to **analyze a network configuration** and correct it.

That makes it a very different kind of challenge inside the 42 journey.

---

## Core Idea

The central idea of **NetPractice** is to understand when communication is possible and when it is not.

In the first levels, the focus is on understanding how an IPv4 address is divided between:

- the **network part**
- and the **host part**

This division depends on the **subnet mask**.

For example, with:

```text
255.255.255.0
````

the first three octets identify the network, while the last octet is used for hosts inside that network.

This also introduces important concepts such as:

* **network address**
* **host range**
* **broadcast**
* **subnets**

As the exercises evolve, the project adds more structure and more devices, such as:

* hosts
* switches
* routers
* internet access paths

So the learning path grows from simple local communication to the first notions of routing and external communication.

---

## Training and Evaluation

The exercises are presented in an **HTML page used for practice and evaluation**.

At first, the user trains through progressive exercises that become more complex over time.

Then, in evaluation mode, the project becomes more intense because the student must solve networking problems under time pressure.

That is one of the reasons why NetPractice is valuable:
it teaches not only the concepts themselves, but also the ability to **reason quickly and correctly** about small network topologies.

---

## IPv4 and Subnet Masks

One of the first major lessons in **NetPractice** is that an IP address is not enough by itself.

It must be interpreted together with its **subnet mask**.

A mask tells us which part of the address belongs to the network and which part belongs to the host.

For example:

```text
IP:   192.168.1.42
Mask: 255.255.255.0
```

This means:

* network: `192.168.1.0`
* valid hosts: `192.168.1.1` to `192.168.1.254`
* broadcast: `192.168.1.255`

So the machine `192.168.1.42` belongs to the subnet `192.168.1.0/24`.

Another important point is that subnet masks can be written in two ways:

```text
255.255.255.0
```

or:

```text
/24
```

Both represent the same thing.

I personally found the dotted notation more visual and easier to calculate by hand, although prefix notation like `/24` or `/30` is also very common and important to understand.

If needed, the project even allows using tools like `bc` to assist with calculations.

---

## Switches, Routers and the Internet

As the project progresses, new devices appear.

### Switches

A **switch** allows multiple machines to communicate inside the same local network.

If the devices are in the same subnet and everything is configured correctly, the communication can happen locally without needing a router.

### Routers

A **router** becomes important when the destination is in another network.

If a machine tries to access an IP that is outside its own subnet, it does not treat that destination as a local neighbor.

Instead, it forwards the traffic to its **default gateway**, which is usually a router.

That router then decides how to continue the communication.

This is one of the most important networking ideas in the project:

* local destination → communicate directly
* remote destination → send to the router

### Internet and provider access

When communication goes beyond the local network, the traffic usually leaves the LAN through the router and continues toward the **ISP** or access provider.

That detail is useful because beginners often get confused when they see an unfamiliar IP in that part of the path.

But that is normal:
before reaching the wider internet, the traffic usually passes through infrastructure managed by the provider.

---

## Practical Examples

Here are some examples that reflect the logic I studied in the project.

### Example 1 — Two machines in the same subnet

```text
Host A: 192.168.1.10 /24
Host B: 192.168.1.20 /24
```

Both belong to:

```text
192.168.1.0/24
```

So they are in the same subnet.

That means they can communicate directly, assuming the topology is correct.

---

### Example 2 — Broadcast and host range

If we have:

```text
IP:   10.0.0.15
Mask: 255.255.255.0
```

then the subnet is:

```text
10.0.0.0/24
```

So:

* subnet address: `10.0.0.0`
* valid host range: `10.0.0.1` to `10.0.0.254`
* broadcast: `10.0.0.255`

That means `10.0.0.15` is a valid host in this network.

---

### Example 3 — Two machines in different networks

```text
Host A: 192.168.1.10 /24
Host B: 192.168.2.20 /24
```

Now the networks are different:

* `192.168.1.0/24`
* `192.168.2.0/24`

So Host A does **not** see Host B as local.

It must send the traffic to the **default gateway**, and the router will decide how to forward it.

Without a correct router path, the communication fails.

---

### Example 4 — Why the router matters

Imagine this:

```text
PC:       10.10.10.5 /24
Gateway:  10.10.10.1 /24
Target:   8.8.8.8
```

The target `8.8.8.8` is clearly outside the local subnet.

So the PC does not try to find `8.8.8.8` directly in the local network.

Instead, it sends the traffic to:

```text
10.10.10.1
```

which is the router.

That router becomes the next step in the path toward the outside network.

---

### Example 5 — A switch connecting local hosts

```text
Host A: 172.16.0.10 /16
Host B: 172.16.5.20 /16
Host C: 172.16.8.30 /16
```

With mask `/16`, all of them belong to:

```text
172.16.0.0/16
```

So if they are connected through a switch, they can communicate inside the same local network.

The switch helps connect multiple devices in the same subnet.

---

### Example 6 — Understanding `/30`

A `/30` subnet is very small.

For example:

```text
192.168.50.0/30
```

This gives four addresses total:

* `192.168.50.0` → network
* `192.168.50.1` → usable host
* `192.168.50.2` → usable host
* `192.168.50.3` → broadcast

That leaves only **two usable addresses**.

This kind of subnet is often useful when studying point-to-point links.

---

### Example 7 — Different masks require attention

Sometimes two IPs may look visually close, but different masks change how each host interprets the network.

For example:

```text
Host A: 192.168.1.10 /24
Host B: 192.168.1.20 /25
```

At first glance, they seem compatible because the numbers look close.

But subnet interpretation depends on the mask, not only on the visible similarity of the IPs.

That is why, in practice, using coherent masks across the same segment avoids many mistakes and confusion.

---

## How To Use

The project is solved through the training interface in the browser.

The usual flow is:

1. open the HTML interface
2. analyze the broken configuration
3. adjust IPs, masks, or routes
4. check whether the communication becomes valid
5. repeat for increasingly complex exercises

Over time, the exercises grow in difficulty and start combining several networking ideas at once.

That progressive structure is what makes the project a very good first contact with networking.

---

## Team

**NetPractice** is an individual project at **École 42**.

So this project was completed by me as part of my networking foundation in the cursus.

---

## Final Note

For me, **NetPractice** was a very important introduction to networking because it transformed abstract concepts into something visible and logical.

It helped me understand:

* how IPv4 addressing works
* how subnet masks divide networks
* why some machines communicate directly and others do not
* when a router becomes necessary
* how local communication differs from external communication
* how the internet path begins from the local gateway and continues through the provider

It is a simple project in appearance, but it gives a real foundation.

And that is exactly what makes it valuable:
it teaches the first mental model a programmer or systems student needs in order to stop seeing a network as magic and start seeing it as structure, logic, and routing decisions.

**Final result:** `net_practice` — **100/100**
**Bonus:** None
**Status:** Completed

