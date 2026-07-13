# 06 -- Memory System

## Purpose

The memory system gives the AI Server Lab the ability to retain and retrieve information over time.

A traditional chatbot only understands the current conversation.

Once the conversation ends:

- Context is lost.
- Previous information is unavailable.
- The user must manually provide information again.

This system uses a separate memory layer that stores, organizes, and retrieves information when needed.

The goal is to create a personal knowledge system that can assist with:

- Business records
- Documents
- Projects
- Notes
- Receipts
- Technical documentation
- Long-term workflows

---

# Memory Architecture

The AI model and memory system are separated.

The model provides intelligence.

The memory system provides knowledge.

```text
                    User

                      |

                      |

                  Odysseus

                      |

                      |

              Retrieval System

                      |

          ----------------------

          |                    |

      ChromaDB             Documents

          |                    |

     Embeddings           Files

          |

          |

     Relevant Context

          |

          |

       Ollama Model

          |

          |

       Response
```

---

# Why Separate Memory From the AI Model?

AI models do not automatically remember information.

Example:

Conversation 1:

```text
User:
My business uses this receipt format.
```

The AI understands the information temporarily.

After the conversation ends:

```text
Memory:

Empty
```

A memory system changes this:

```text
Conversation

      |

      |

Important Information Identified

      |

      |

Stored in Database

      |

      |

Available Later
```

---

# Memory Components

The AI Server Lab memory system contains several layers.

| Component | Purpose |
|---|---|
| Documents | Original files and records |
| OCR | Converts images into text |
| Embeddings | Converts information into searchable data |
| Vector Database | Stores searchable memory |
| Retrieval System | Finds relevant information |
| AI Model | Generates responses |

---

# Retrieval-Augmented Generation (RAG)

The memory system uses a process called:

```
Retrieval-Augmented Generation
```

or:

```
RAG
```

Instead of sending every document to the AI model, the system searches memory and only provides relevant information.

---

# RAG Workflow

Example:

User asks:

```text
How much did I spend on fuel this year?
```

The system performs:

```text
Question

   |

   ↓

Memory Search

   |

   ↓

Relevant Documents Found

   |

   ↓

Information Sent To AI

   |

   ↓

Response Generated
```

---

# Traditional AI vs Memory AI

## Traditional Chatbot

```text
Question

   |

AI Model

   |

Answer
```

Limitations:

- No long-term knowledge
- Limited context
- Requires repeated information

---

## Memory-Enabled AI

```text
Question

   |

Memory Search

   |

Relevant Information

   |

AI Model

   |

Answer
```

Benefits:

- Long-term knowledge
- Better accuracy
- Lower token usage
- Larger information capacity

---

# ChromaDB

ChromaDB is used as the vector database.

Its purpose:

- Store embeddings
- Search documents
- Retrieve relevant information

Architecture:

```text
Documents

    |

    |

Embeddings

    |

    |

ChromaDB

    |

    |

Relevant Context
```

---

# What Are Embeddings?

Embeddings convert information into numerical representations.

Example:

Text:

```text
Fuel receipt from January
```

becomes:

```text
[0.234, 0.982, 0.451, ...]
```

The numbers allow the database to find similar information.

The system searches by meaning instead of exact words.

---

# Document Memory Workflow

Example:

A receipt is uploaded.

```text
Receipt Image

      |

      |

OCR Processing

      |

      |

Extracted Text

      |

      |

Embedding Creation

      |

      |

ChromaDB Storage

      |

      |

Available To AI
```

---

# Business Receipt Example

A user uploads:

```text
Receipts/

├── January

├── February

└── March
```

The system processes:

```text
Receipt Image

      |

OCR

      |

Date Extraction

      |

Business Category

      |

Amount

      |

Memory Storage
```

Example stored information:

```text
Date:
01/15/2026

Category:
Fuel

Amount:
$72.45

Vendor:
Example Station
```

---

# Memory Storage Design

The AI Server Lab uses:

```text
AI-Server-Lab

├── data

│

├── documents

│

├── chromadb

│

└── odysseus
```

Purpose:

| Location | Function |
|---|---|
| documents | Original files |
| chromadb | Searchable memory |
| odysseus | User interface data |

---

# Memory Security

Memory systems may contain sensitive information:

- Financial records
- Business information
- Personal documents
- Family records

Security practices:

✅ Keep storage local  
✅ Use encrypted remote access  
✅ Maintain backups  
✅ Restrict device access  
✅ Avoid public database exposure  

---

# Backup Strategy

Important data:

```text
Documents

+

ChromaDB Database

+

Configuration Files
```

should be backed up.

Recommended structure:

```text
backups/

├── documents/

├── chromadb/

└── configuration/
```

---

# Future Memory Expansion

The system can eventually store:

## Business Knowledge

- Procedures
- Customer information
- Reports
- Expenses


## Technical Knowledge

- Documentation
- Projects
- Configurations
- Troubleshooting


## Personal Knowledge

- Notes
- Important records
- Planning documents

---

# Complete AI Memory Architecture

```text
                         User

                          |

                          |

                      Odysseus

                          |

                          |

                 Retrieval System

                          |

              ----------------------

              |                    |

          ChromaDB             Files

              |                    |

        Vector Search            OCR

              |

              |

        Relevant Information

              |

              |

           Ollama Model

              |

              |

           AI Response
```

---

# Memory Validation Complete

At this stage:

| Component | Status |
|---|---|
| Memory Architecture Designed | ✅ Ready |
| ChromaDB Planned | ✅ Ready |
| Document Storage Planned | ✅ Ready |
| RAG Workflow Defined | ✅ Ready |
| Backup Strategy Defined | ✅ Ready |

The AI system now has the foundation for long-term knowledge retention.

---

# Next Step

Continue to:

```
07 -- Document Processing and OCR
```

The next stage will build the workflow for converting real-world files such as receipts, images, and PDFs into searchable AI knowledge.