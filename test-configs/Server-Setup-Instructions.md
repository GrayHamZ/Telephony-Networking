# Server Setup Instructions

## Server: DNS/Web/Email Server

### Network Configuration

**Server Details:**
- **Hostname**: Server-Test
- **IP Address**: 192.168.150.8
- **Subnet Mask**: 255.255.255.0
- **Default Gateway**: 192.168.150.1
- **VLAN**: 150 (Department H Data VLAN)
- **Connected to**: SW-Test-6 Port fa0/21

---

## Initial Server Configuration in Packet Tracer

### Step 1: Configure IP Settings
1. Click on the **Server** device
2. Go to the **Desktop** tab
3. Click on **IP Configuration**
4. Select **Static**
5. Enter the following:
   - **IP Address**: `192.168.150.8`
   - **Subnet Mask**: `255.255.255.0`
   - **Default Gateway**: `192.168.150.1`
   - **DNS Server**: `192.168.150.8` (itself)

---

## DNS Service Configuration

### Step 1: Enable DNS Service
1. Click on the **Server** device
2. Go to the **Services** tab
3. Click on **DNS**
4. Turn **DNS Service** to **ON**

### Step 2: Add DNS Records
Add the following A Records for all departments:

#### Router Records
| Name | Type | Address |
|------|------|---------|
| router1.local | A | 192.168.10.2 |
| router2.local | A | 192.168.10.3 |

#### Department Records
| Name | Type | Address |
|------|------|---------|
| dept-a.local | A | 192.168.10.1 |
| dept-b.local | A | 192.168.30.1 |
| dept-c.local | A | 192.168.50.1 |
| dept-d.local | A | 192.168.70.1 |
| dept-e.local | A | 192.168.90.1 |
| dept-f.local | A | 192.168.110.1 |
| dept-g.local | A | 192.168.130.1 |
| dept-h.local | A | 192.168.150.1 |

#### Server Records
| Name | Type | Address |
|------|------|---------|
| server.local | A | 192.168.150.8 |
| mail.local | A | 192.168.150.8 |
| www.local | A | 192.168.150.8 |
| dns.local | A | 192.168.150.8 |

**To Add a DNS Record:**
1. Enter the **Name** (e.g., `server.local`)
2. Select **Type**: `A Record`
3. Enter the **Address** (e.g., `192.168.150.8`)
4. Click **Add**

---

## HTTP/HTTPS Service Configuration

### Step 1: Enable HTTP Service
1. Go to **Services** > **HTTP**
2. Turn **HTTP Service** to **ON**
3. Turn **HTTPS Service** to **ON** (if available)

### Step 2: Create Web Pages
You can create custom web pages by editing the `index.html` file:

**Sample Welcome Page:**
```html
<html>
<head><title>Welcome to Test Network</title></head>
<body>
<h1>Test Network Server</h1>
<h2>Available Services</h2>
<ul>
  <li>DNS Service</li>
  <li>Web Hosting</li>
  <li>Email Service (SMTP/POP3/IMAP)</li>
</ul>
<h3>Server Information</h3>
<p>IP Address: 192.168.150.8</p>
<p>Server Location: Department H (VLAN 150)</p>
<p>All departments can access this server via inter-VLAN routing.</p>
</body>
</html>
```

### Step 3: Test Web Service
From any PC in the network:
1. Open a **Web Browser**
2. Enter the server IP: `http://192.168.150.8`
3. Or use DNS: `http://server.local` or `http://www.local`

---

## Email Service Configuration

### Step 1: Enable Email Services
1. Go to **Services** > **EMAIL**
2. Turn **SMTP** to **ON** (Sending Email)
3. Turn **POP3** to **ON** (Receiving Email)
4. Turn **IMAP** to **ON** (if available)

**Service Ports:**
- **SMTP**: Port 25 (Outgoing mail)
- **POP3**: Port 110 (Incoming mail)
- **IMAP**: Port 143 (Incoming mail)

### Step 2: Create Email Accounts
Create email accounts for each department:

#### Department A Users
- **Username**: `user1.deptA`
- **Password**: `password`

#### Department B Users
- **Username**: `user1.deptB`
- **Password**: `password`

#### Department C Users
- **Username**: `user1.deptC`
- **Password**: `password`

#### Department D Users
- **Username**: `user1.deptD`
- **Password**: `password`

#### Department E Users
- **Username**: `user1.deptE`
- **Password**: `password`

#### Department F Users
- **Username**: `user1.deptF`
- **Password**: `password`

#### Department G Users
- **Username**: `user1.deptG`
- **Password**: `password`

#### Department H Users
- **Username**: `user1.deptH`
- **Password**: `password`

**To Create an Email Account:**
1. Under **EMAIL** service
2. Enter the **Username** (e.g., `user1.deptA`)
3. Enter the **Password** (e.g., `password`)
4. Click **+** or **Add** button
5. Repeat for all users

---

## How to Use Email Service

### From a PC or Laptop:

#### Step 1: Configure Email Client
1. Click on a **PC** or **Laptop** device
2. Go to **Desktop** tab
3. Click on **Email**
4. Click on **Email Configuration**

#### Step 2: Enter Email Settings

**For User in Department A:**
- **Email Address**: `user1.deptA@192.168.150.8`
- **Display Name**: `User 1 Department A`
- **Incoming Mail Server**: `192.168.150.8` (or `mail.local`)
- **Outgoing Mail Server**: `192.168.150.8` (or `mail.local`)
- **Username**: `user1.deptA`
- **Password**: `password`

**For User in Department B:**
- **Email Address**: `user1.deptB@192.168.150.8`
- **Display Name**: `User 1 Department B`
- **Incoming Mail Server**: `192.168.150.8`
- **Outgoing Mail Server**: `192.168.150.8`
- **Username**: `user1.deptB`
- **Password**: `password`

*Repeat similar configuration for all departments.*

#### Step 3: Compose and Send Email
1. Click **Compose** button
2. Enter the recipient's email address: `user1.deptB@192.168.150.8`
3. Enter **Subject**: `Test Email`
4. Enter **Message**: `Hello from Department A!`
5. Click **Send**

#### Step 4: Receive Email
1. Click **Receive** button
2. The email will appear in the inbox
3. Click on the email to read it

---

## Testing Server Connectivity

### Test 1: Ping Server from Different VLANs
From any PC in the network:
1. Open **Command Prompt**
2. Type: `ping 192.168.150.8`
3. You should receive replies from the server

### Test 2: DNS Resolution
From any PC:
1. Open **Command Prompt**
2. Type: `ping server.local`
3. It should resolve to `192.168.150.8` and receive replies

### Test 3: Web Access
From any PC:
1. Open **Web Browser**
2. Type: `http://192.168.150.8` or `http://server.local`
3. The web page should load

### Test 4: Email Communication
1. Configure email on PC in Department A
2. Configure email on PC in Department B
3. Send email from Department A to Department B
4. Verify email is received in Department B

---

## Troubleshooting

### Server Not Reachable
1. **Check Server IP Configuration**
   - Verify IP: 192.168.150.8
   - Verify Gateway: 192.168.150.1
   
2. **Check Switch Port**
   - Verify SW-Test-6 fa0/21 is configured correctly
   - Port should be access mode on VLAN 150

3. **Check VLAN Configuration**
   - Verify VLAN 150 exists on SW-Test-6 and MLS-Test-2
   - Verify trunk links allow VLAN 150

4. **Check Router Configuration**
   - Verify sub-interface g0/0.150 on both routers
   - Verify HSRP is active
   - Verify OSPF is advertising 192.168.150.0/24

### DNS Not Resolving
1. Verify DNS service is **ON** on the server
2. Check DNS records are added correctly
3. Verify PCs have DNS server set to 192.168.150.8 (should be automatic via DHCP)

### Email Not Working
1. Verify SMTP and POP3/IMAP services are **ON**
2. Verify email accounts are created on the server
3. Check email client configuration on PC
4. Verify username format matches: `username@192.168.150.8`

### Web Page Not Loading
1. Verify HTTP service is **ON**
2. Check if the server is reachable (ping test)
3. Try using IP address instead of DNS name
4. Verify firewall rules (if any) allow HTTP traffic

---

## Network Diagram Reference

```
                    Router-Test-1 (Active HSRP)
                            |
                       MLS-Test-1 ←→ MLS-Test-2
                            |              |
                    (Multiple Switches)    |
                                          |
                                     SW-Test-6
                                          |
                    fa0/1-10: Department F (VLAN 110/120)
                    fa0/11-20: Department H (VLAN 150/160)
                    fa0/21: DNS/Web/Email Server (VLAN 150)
                            |
                    Server: 192.168.150.8
```

---

## Server Services Summary

| Service | Port | Status | Purpose |
|---------|------|--------|---------|
| DNS | 53 | ON | Domain name resolution |
| HTTP | 80 | ON | Web hosting |
| HTTPS | 443 | ON | Secure web hosting |
| SMTP | 25 | ON | Send emails |
| POP3 | 110 | ON | Receive emails |
| IMAP | 143 | ON | Receive emails (alternative) |

---

## Additional Notes

- All 8 departments (A-H) can access the server
- The server is on VLAN 150 but accessible from all VLANs via inter-VLAN routing
- HSRP provides redundancy - if Router-Test-1 fails, Router-Test-2 takes over
- The server IP (192.168.150.8) is excluded from DHCP to prevent conflicts
- All DHCP pools point to this server as the DNS server

---

## Created by: Network Administrator
## Date: December 2, 2025
## Network: Test Topology - IP Telephony with HSRP Redundancy
