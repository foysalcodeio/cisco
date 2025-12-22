


নিচে দেওয়া `running-config` এর প্রতিটি অংশ **কি কাজ করে** তা সহজ বাংলায় বিস্তারিতভাবে ব্যাখ্যা করা হলো। এটি CCNA / Lab Practice / Interview preparation এর জন্য উপযোগী।

---

## 1. Basic Information

```
Building configuration...
Current configuration : 611 bytes
```

* Router এর বর্তমান configuration RAM এ আছে
* Config size = 611 bytes

---

## 2. IOS Version

```
version 15.1
```

* Router এ Cisco IOS version 15.1 চলছে
* IOS হলো router এর operating system

---

## 3. Service Timestamp (Disabled)

```
no service timestamps log datetime msec
no service timestamps debug datetime msec
```

* Log ও debug message এ time দেখাবে না
* Troubleshooting এর সময় সাধারণত enable করা ভালো

---

## 4. Password Encryption (Disabled)

```
no service password-encryption
```

* Password plain text আকারে থাকবে
* Security কম
* Production network এ এটি **enable করা উচিত**

Command:

```
service password-encryption
```

---

## 5. Hostname

```
hostname Router
```

* Router এর নাম = `Router`
* Default hostname

---

## 6. Cisco Express Forwarding (CEF) Disabled

```
no ip cef
no ipv6 cef
```

* CEF হলো fast packet forwarding mechanism
* Disable থাকলে router ধীরগতিতে packet forward করে
* Real network এ **CEF enable রাখা উচিত**

---

## 7. License Information

```
license udi pid CISCO1941/K9 sn FTX15242G9K-
```

* Router model: **Cisco 1941**
* Serial number উল্লেখ করা আছে
* Licensing verification এর জন্য ব্যবহৃত

---

## 8. Spanning Tree Protocol

```
spanning-tree mode pvst
```

* PVST = Per VLAN Spanning Tree
* Network loop prevent করে
* Layer 2 network এ broadcast storm রোধ করে

---

## 9. Interface Configuration

### ▶ GigabitEthernet0/0

```
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 shutdown
```

ব্যাখ্যা:

* Interface এ কোনো IP address দেওয়া হয়নি
* Duplex & Speed auto negotiation
* `shutdown` → Port OFF অবস্থায় আছে

---

### ▶ GigabitEthernet0/1

```
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
```

ব্যাখ্যা:

* এটিও inactive interface
* IP assign করা হয়নি

---

### ▶ VLAN Interface

```
interface Vlan1
 no ip address
 shutdown
```

ব্যাখ্যা:

* Default management VLAN
* সাধারণত switch management এর জন্য ব্যবহৃত
* Router এ এটি shutdown অবস্থায়

---

## 10. IP Classless Routing

```
ip classless
```

* Classless routing enable
* Subnet mask ignore না করে best route খোঁজে
* Modern network এ default enable থাকে

---

## 11. NetFlow Export

```
ip flow-export version 9
```

* Traffic analysis এর জন্য NetFlow version 9
* Monitoring / accounting কাজে ব্যবহৃত

---

## 12. Line Configuration

### ▶ Console Line

```
line con 0
```

* Physical console access
* Local configuration এর জন্য ব্যবহৃত
* কোনো password দেওয়া নেই

---

### ▶ AUX Line

```
line aux 0
```

* Modem dial-up access এর জন্য (পুরনো প্রযুক্তি)
* সাধারণত unused থাকে

---

### ▶ VTY Lines (Remote Access)

```
line vty 0 4
 login
```

ব্যাখ্যা:

* Remote login port (0–4) → মোট 5 জন user
* `login` command আছে
* কিন্তু **password / transport input নেই**

⚠️ তাই Telnet / SSH কাজ করবে না

Correct configuration উদাহরণ:

```
line vty 0 4
 password cisco
 login
 transport input telnet ssh
```

---

## 13. Missing / Weak Config (Important Notes)

❌ No IP address on interfaces
❌ All ports shutdown
❌ No enable secret
❌ No console password
❌ Password encryption disabled
❌ SSH/Telnet incomplete

---

## 14. Recommended Basic Secure Config

```
service password-encryption
enable secret StrongPass
line con 0
 password console123
 login
line vty 0 4
 password vty123
 login
 transport input ssh
```

---

## 15. Overall Summary

| Section       | Status     |
| ------------- | ---------- |
| IOS           | OK         |
| Interfaces    | OFF        |
| IP Addressing | Missing    |
| Security      | Weak       |
| Remote Access | Incomplete |

---

## ✅ Conclusion

এই configuration টি মূলত **fresh / default router config**।
এটি production-ready না।

📌 Practice করার জন্য perfect, কিন্তু real network এ deploy করার আগে security ও IP configuration দরকার।
