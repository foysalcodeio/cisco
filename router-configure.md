# Cisco Router – Running Configuration Explanation (Bangla)

এই README.md ফাইলটি Cisco Router (IOS) এর **basic modes, passwords, configuration, save/reload, এবং interface setup** সহজভাবে বুঝানোর জন্য সাজানো হয়েছে। GitHub এ নোট/রেফারেন্স হিসেবে ব্যবহার করার জন্য উপযুক্ত।

---

## 1. Router Modes (Execution Modes)

### ▶ User EXEC Mode

```
Router>
```

* Limited access
* শুধু **monitoring** করা যায়
* Configuration করা যায় না

### ▶ Privileged EXEC Mode

```
Router> enable
Router#
```

* Administrator mode
* Configuration, debug, show commands ব্যবহার করা যায়

---

## 2. Configuration Modes

### ▶ Global Configuration Mode

```
Router# configure terminal
Router(config)#
```

* Router এর overall configuration

### ▶ Sub Configuration Modes

#### Console Line Mode

```
Router(config)# line con 0
Router(config-line)#
```

#### VTY Line Mode (Remote Access)

```
Router(config)# line vty 0 4
```

* Virtual Teletype
* মোট 5টি port (0–4)
* Remote login এর জন্য ব্যবহার হয়
* Protocol: `telnet`, `ssh`

---

## 3. Important Show Commands

| Command               | Description                   |
| --------------------- | ----------------------------- |
| `show running-config` | RAM থেকে current config দেখায় |
| `show startup-config` | NVRAM থেকে saved config দেখায় |
| `show flash:`         | Flash memory এর content দেখায় |

---

## 4. IOS Service Commands

### ▶ Disable Service (Comment এর মত)

```
no service timestamps log datetime msec
```

* Service active থাকে না

### ▶ Spanning Tree

```
spanning-tree mode pvst
```

* Loop prevent করার জন্য
* Continuous loop বন্ধ করে

---

## 5. Hostname Configuration

Linux: `touch`
Windows: `mkdir`
Cisco IOS equivalent:

```
Router(config)# hostname Dhaka-North
```

Result:

```
Dhaka-North>
```

---

## 6. Console Password Configuration

```
Dhaka-North> enable
Dhaka-North# configure terminal
Dhaka-North(config)# line con 0
Dhaka-North(config-line)# password 123
Dhaka-North(config-line)# login
Dhaka-North(config-line)# exit
```

> ⚠️ `login` না দিলে password কাজ করবে না

---

## 7. Enable Password vs Enable Secret

### ▶ Enable Password

```
Dhaka-North(config)# enable password 456
```

### ▶ Enable Secret (Recommended & Strong)

```
Dhaka-North(config)# enable secret asd
```

Example (Encrypted):

```
enable secret 5 $1$mERr$1A6WmlgXdpa7HsGQy66Qd1
```

✅ `enable secret` থাকলে `enable password` ignore হয়

---

## 8. Password Encryption (Plain → Encrypted)

```
Dhaka-North(config)# service password-encryption
```

* সব plain text password encrypted হয়ে যায়

---

## 9. Change / Remove Password

### ▶ Change Console Password

```
configure terminal
line con 0
password NEW_PASSWORD
```

### ▶ Remove Password

```
configure terminal
line con 0
no password
```

---

## 10. User vs Privileged Mode Summary

| Mode            | Prompt                 |
| --------------- | ---------------------- |
| User EXEC       | `Router>`              |
| Privileged EXEC | `Router#`              |
| Global Config   | `Router(config)#`      |
| Line Config     | `Router(config-line)#` |

---

## 11. Save Configuration

### ▶ RAM → NVRAM

```
copy running-config startup-config
```

### ▶ Shortcut Commands

```
write memory
write
wr
```

---

## 12. Restart Router

```
reload
```

---

## 13. Interface & IP Configuration

```
Router# configure terminal
Router(config)# hostname Dhaka-North
Dhaka-North(config)# interface GigabitEthernet0/0
Dhaka-North(config-if)# ip address 192.168.1.1 255.255.255.0
Dhaka-North(config-if)# no shutdown
Dhaka-North(config-if)# description To-LAN-SW
```

* `no shutdown` → Port ON করে
* `description` → Documentation purpose

---

## 14. Memory Types Summary

| Memory | Usage                 |
| ------ | --------------------- |
| RAM    | Running Configuration |
| NVRAM  | Startup Configuration |
| Flash  | IOS Image             |

---

## ✅ End Notes
