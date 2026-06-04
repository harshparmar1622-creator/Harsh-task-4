# Task 4: Setup and Use a Firewall on Ubuntu Linux Using UFW

## Objective

Configure and test basic firewall rules to allow or block network traffic using UFW (Uncomplicated Firewall) on Ubuntu Linux.

---

## Tools Used

* Ubuntu Linux
* UFW (Uncomplicated Firewall)
* Telnet
* Netcat (nc)

---

## Procedure

### 1. Verify UFW Installation

```bash
sudo apt update
sudo apt install ufw -y
```

Result: UFW was already installed on the system.

---

### 2. Check Firewall Status

```bash
sudo ufw status verbose
```

Output:

```text
Status: inactive
```

---

### 3. Configure Default Firewall Policies

Block all incoming connections by default and allow outgoing connections.

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

---

### 4. Allow SSH Traffic (Port 22)

```bash
sudo ufw allow 22/tcp
```

Result:

```text
Rules updated
Rules updated (v6)
```

---

### 5. Enable the Firewall

```bash
sudo ufw enable
```

Result:

```text
Firewall is active and enabled on system startup
```

---

### 6. Display Current Firewall Rules

```bash
sudo ufw status numbered
```

Output:

```text
22/tcp ALLOW IN Anywhere
```

---

### 7. Block Telnet Port (Port 23)

```bash
sudo ufw deny 23/tcp
```

Result:

```text
Rule added
Rule added (v6)
```

---

### 8. Test the Firewall Rule

#### Using Telnet

```bash
telnet localhost 23
```

Output:

```text
Trying 127.0.0.1...
Unable to connect to remote host: Connection refused
```

#### Using Netcat

```bash
nc -zv localhost 23
```

Output:

```text
connect to localhost (127.0.0.1) port 23 failed: Connection refused
```

These results indicate that Port 23 is inaccessible.

---

### 9. Remove the Test Rule

```bash
sudo ufw delete deny 23/tcp
```

Result:

```text
Rule deleted
Rule deleted (v6)
```

---

### 10. Enable Firewall Logging

```bash
sudo ufw logging on
```

View logs:

```bash
sudo tail -f /var/log/ufw.log
```

Sample log entry:

```text
[UFW BLOCK]
```

This confirms that the firewall is actively blocking unwanted traffic.

---

### 11. Restore Original Configuration

Disable and reset the firewall.

```bash
sudo ufw disable
sudo ufw reset
```

Result:

```text
Firewall stopped and disabled on system startup
Resetting all rules to installed defaults
```

---

## Interview Questions and Answers

### 1. What is a Firewall?

A firewall is a security system that monitors and filters incoming and outgoing network traffic based on predefined security rules.

### 2. Difference Between Stateful and Stateless Firewall?

* Stateful firewalls track active network connections and make decisions based on connection state.
* Stateless firewalls inspect each packet independently without maintaining connection information.

### 3. What Are Inbound and Outbound Rules?

* Inbound rules control traffic entering the system.
* Outbound rules control traffic leaving the system.

### 4. How Does UFW Simplify Firewall Management?

UFW provides a simple command-line interface for managing firewall rules without directly configuring complex iptables rules.

### 5. Why Block Port 23 (Telnet)?

Telnet transmits data, including usernames and passwords, in plain text, making it insecure and vulnerable to interception.

### 6. What Are Common Firewall Mistakes?

* Blocking SSH access accidentally
* Allowing unnecessary ports
* Ignoring firewall logs
* Creating overly permissive rules
* Not testing configurations

### 7. How Does a Firewall Improve Network Security?

A firewall protects systems by blocking unauthorized access, filtering malicious traffic, and reducing the attack surface.

### 8. What Is NAT in Firewalls?

Network Address Translation (NAT) translates private IP addresses into public IP addresses, allowing multiple devices to share a single public IP address while improving security.

---

## Conclusion

In this task, UFW was configured and tested on Ubuntu Linux. Default firewall policies were applied, SSH traffic was allowed, and Telnet traffic on port 23 was blocked. The firewall rules were verified through testing and logging. Finally, the temporary rules were removed, and the firewall configuration was restored to its original state. This task provided practical experience in firewall configuration, network traffic filtering, and basic system security management.
