# 05 -- Tailscale Remote Access

## Purpose

Tailscale provides secure remote access to the AI Server Lab without exposing services directly to the public internet.

This allows devices such as:

- iPad
- Laptop
- Phone
- Additional workstations

to securely connect to the AI server from anywhere.

The goal is to create a private network where trusted devices can communicate as if they were on the same local network.

---

# Why Tailscale?

Traditional remote access requires:

- Port forwarding
- Public IP addresses
- Firewall configuration
- Router changes
- Internet-facing services

This creates unnecessary security risks.

Tailscale replaces this with a private encrypted network.

---

# Traditional Remote Access

Example:

```text
Internet

   |

   |

Router Port Forward

   |

   |

AI Server

   |

   |

Service
```

Problems:

- Services are exposed publicly.
- Attack surface increases.
- Router configuration required.
- IP addresses may change.

---

# Tailscale Remote Access

The preferred architecture:

```text
                iPad

                 |

                 |

          Encrypted Tailnet

                 |

                 |

             AI Server

                 |

                 |

             Services
```

Benefits:

- No open internet ports
- Encrypted communication
- Device authentication
- Private IP addresses
- Easy device management

---

# Understanding Tailscale

Tailscale creates a private network called a:

```
Tailnet
```

Each authorized device receives a private Tailscale IP.

Example:

```text
AI Server

100.x.x.10


iPad

100.x.x.20
```

The devices communicate through the encrypted network.

---

# Installation

## Install on AI Server

Install Tailscale:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

Verify:

```bash
tailscale version
```

---

# Authenticate Server

Start Tailscale:

```bash
sudo tailscale up
```

A browser window will open.

Sign in using your Tailscale account.

---

# Verify Server Connection

Check status:

```bash
tailscale status
```

Example:

```text
100.x.x.10

ai-server

connected
```

---

# Install Tailscale on iPad

Install the Tailscale application.

Sign in using the same account as the AI server.

After connecting:

The iPad becomes part of the same private network.

---

# Test Connectivity

From the AI server:

```bash
tailscale ip
```

Example:

```text
100.x.x.10
```

This is the server's private Tailscale address.

---

# Network Test

From another device:

Ping the server:

```bash
ping 100.x.x.10
```

Successful replies confirm:

- Device authentication works.
- Tailnet communication works.
- Encryption is active.

---

# Connecting to AI Services

Once Tailscale is active, services can be accessed privately.

Example:

```text
iPad Browser

       |

       |

http://100.x.x.10:3000

       |

       |

Odysseus
```

The connection path:

```text
iPad

 |

 |

Encrypted Tailscale Network

 |

 |

AI Server

 |

 |

Odysseus Container

 |

 |

Ollama
```

---

# Ollama Security Design

Ollama should NOT be exposed directly.

Bad:

```text
Internet

    |

    |

Port 11434

    |

    |

Ollama
```

Good:

```text
iPad

    |

    |

Tailscale

    |

    |

AI Server

    |

    |

Ollama
```

The AI server remains private.

---

# Tailscale and Docker

Docker services can communicate with Tailscale in several ways.

Common approaches:

## Option 1 -- Access Through Host

Example:

```text
iPad

 |

 |

Tailscale IP

 |

 |

Host Machine

 |

 |

Docker Container
```

Simple and recommended for this lab.

---

## Option 2 -- Run Tailscale Inside Docker

Example:

```text
Docker

├── Tailscale Container
│
├── Odysseus Container
│
└── Ollama Container
```

More advanced.

Useful for dedicated servers.

---

# Device Management

A Tailnet should only contain trusted devices.

Recommended devices:

```text
Approved Devices

├── AI Server
├── Dad's iPad
├── Personal Laptop
└── Future Devices
```

Remove devices that are no longer trusted.

---

# Security Recommendations

## Do:

✅ Use device authentication  
✅ Enable multi-factor authentication  
✅ Keep Tailscale updated  
✅ Only add trusted devices  
✅ Keep services private  

---

## Avoid:

❌ Port forwarding  
❌ Public Ollama access  
❌ Exposing Docker ports publicly  
❌ Sharing Tailnet access unnecessarily  

---

# Future AI Workflow

With Tailscale installed:

```text
                    Dad's iPad

                        |

                        |

                  Tailscale VPN

                        |

                        |

                   AI Server

                        |

        --------------------------------

        |                              |

    Odysseus                       Ollama

        |                              |

    Interface                     AI Models

                        |

                        |

                 Memory System
```

---

# Troubleshooting

## Cannot Connect to Server

Check:

```bash
tailscale status
```

Verify:

- Both devices are logged into the same account.
- Tailscale is running.
- Device is approved.

---

## Cannot Access Odysseus

Test locally first:

```text
http://localhost:3000
```

Then remotely:

```text
http://TAILSCALE-IP:3000
```

Example:

```text
http://100.x.x.10:3000
```

---

## Tailscale IP Changed

Check:

```bash
tailscale ip
```

Update the address used by remote devices.

---

# Tailscale Validation Complete

At this stage:

| Component | Status |
|---|---|
| Tailscale Installed | ✅ Ready |
| Server Authenticated | ✅ Ready |
| iPad Connected | ✅ Ready |
| Private Network Created | ✅ Ready |
| Remote Access Tested | ✅ Ready |

The AI server can now be accessed securely without exposing services to the internet.

---

# Current Architecture

```text
                         iPad

                          |

                          |

                     Tailscale

                          |

                          |

                      AI Server

                          |

              ---------------------

              |                   |

          Odysseus            Ollama

              |                   |

          Interface           AI Models
```

---

# Next Step

Continue to:

```
06 -- Memory System
```

The next stage adds persistent knowledge using databases and document retrieval.