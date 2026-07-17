# AI Stack
> *Understanding how my locally hosted AI system is built, how each component communicates, and who is responsible for what.*

---

## 🎯 Purpose

This AI stack is designed to provide a **fully local AI assistant**. Rather than sending prompts to a cloud provider, every request is processed on hardware that I control.

Each service has **one specific responsibility**, allowing components to be upgraded, replaced, or expanded without rebuilding the entire system.

> **Engineering Principle**
>
> *A well-designed system is composed of simple components that each perform one job well.*

---

# 🏗️ System Architecture

```text
┌────────────────────────────────────────────┐
│              User (Browser)                │
└────────────────┬───────────────────────────┘
                 │ HTTP (localhost)
                 ▼
┌────────────────────────────────────────────┐
│             Odysseus (Web UI)              │
│────────────────────────────────────────────│
│ • Chat Interface                           │
│ • Conversation History                     │
│ • Memory Management                        │
│ • Search Integration                       │
└────────────────┬───────────────────────────┘
                 │ Docker Network
                 │ REST API
                 ▼
┌────────────────────────────────────────────┐
│             Ollama Server                  │
│────────────────────────────────────────────│
│ • Serves AI Models                         │
│ • Generates Responses                      │
│ • REST API (:11434)                        │
└────────────────┬───────────────────────────┘
                 │ Loads
                 ▼
┌────────────────────────────────────────────┐
│             Gemma 3:4B Model               │
│────────────────────────────────────────────│
│ • Neural Network Weights                   │
│ • Performs Inference                       │
│ • Stored on Disk                           │
└────────────────────────────────────────────┘
```

---

# 🧩 Components

---

## 🌐 Browser

### Purpose

Provides the graphical interface that allows me to communicate with my AI.

### Responsibilities

- Display the chat interface
- Send prompts
- Display responses

### Does **NOT**

- Run AI models
- Store memory
- Generate responses

---

## 💬 Odysseus

### Purpose

Acts as the **front-end** of the AI stack.

Think of Odysseus as the receptionist.

It accepts my prompt, organizes conversations, stores memory, and sends requests to Ollama.

### Responsibilities

- Chat interface
- Conversation history
- Memory
- Prompt management
- Search
- Connect to Ollama

### Does **NOT**

- Think
- Run the AI model
- Generate text

---

## 🐳 Docker

### Purpose

Docker provides isolated environments called **containers**.

Each service lives inside its own container and communicates over Docker's virtual network.

### Responsibilities

- Run containers
- Create virtual networking
- Isolate applications
- Manage volumes
- Manage images

### Does **NOT**

- Run AI
- Generate text
- Store conversations

---

## 🦙 Ollama

### Purpose

Ollama is the **AI server**.

It loads AI models into memory and exposes a REST API that applications can communicate with.

### Responsibilities

- Load models
- Serve REST API
- Receive prompts
- Stream generated tokens
- Manage installed models

### Does **NOT**

- Provide a chat interface
- Store conversations
- Remember users

---

## 🤖 Gemma 3

### Purpose

Gemma is the **actual AI**.

This neural network performs inference and predicts one token at a time.

### Responsibilities

- Read prompt
- Predict next token
- Generate responses

### Does **NOT**

- Know who I am
- Store memory
- Manage conversations
- Display responses

---

# 🔄 Request Flow

Every prompt follows the same path.

```text
Browser
    │
    ▼
Odysseus
    │
REST API
    │
Docker Network
    │
    ▼
Ollama
    │
Loads Model
    ▼
Gemma 3
    │
Generates Tokens
    ▼
Ollama
    │
Returns Response
    ▼
Odysseus
    │
Displays Chat
    ▼
Browser
```

> **Important**
>
> Every arrow is a **network request (API call)**.
>
> No AI model files are copied between services.

---

# 🗂️ Who Owns What?

| Component | Owns |
|------------|------|
| Windows | Projects, files, source code |
| Docker | Containers, images, networks, volumes |
| Odysseus | Chats, memory, configuration |
| Ollama | AI models |
| Gemma | Neural network weights |

---

# 🧠 Mental Model

Imagine a restaurant.

```text
You
 │
 ▼
Waiter (Odysseus)
 │
 ▼
Kitchen (Ollama)
 │
 ▼
Chef (Gemma)
```

You never speak directly to the chef.

The waiter writes your order.

The kitchen delivers it.

The chef prepares the meal.

The waiter returns with the finished product.

---

# 📡 Communication

Every service communicates over Docker's internal network.

```text
Browser

↓

localhost:3000

↓

Odysseus

↓

host.docker.internal:11434

↓

Ollama API

↓

Gemma

↓

Response

↓

Odysseus

↓

Browser
```

---

# 🧱 System Philosophy

Each service should have **one responsibility**.

| Service | Job |
|-----------|-----|
| Browser | User Interface |
| Odysseus | Chat Management |
| Docker | Infrastructure |
| Ollama | AI Server |
| Gemma | Intelligence |

This separation makes the system:

- Easier to troubleshoot
- Easier to upgrade
- Easier to replace components
- Easier to scale

---

# 💡 Key Takeaways

✅ Docker is **not** AI.

✅ Odysseus is **not** AI.

✅ Ollama is **not** the AI model.

✅ Gemma is the AI model.

✅ Docker only allows the services to communicate.

✅ Every request travels across the Docker network.

---

# 📚 Check on Learning

<details>

<summary><strong>❓ What component actually generates the response?</strong></summary>

**Answer**

Gemma 3 generates the response.

Ollama simply loads the model and provides access to it through an API.

Odysseus displays the response.

</details>

---

<details>

<summary><strong>❓ Why doesn't Odysseus contain the AI?</strong></summary>

**Answer**

Odysseus is only a user interface.

Its job is to organize conversations, manage memory, and communicate with Ollama.

The AI model lives inside Ollama.

</details>

---

<details>

<summary><strong>❓ What is Docker's job?</strong></summary>

**Answer**

Docker creates isolated containers for each application and provides networking between them.

Docker does not perform AI inference.

</details>

---

<details>

<summary><strong>❓ What happens after I press Enter?</strong></summary>

**Answer**

1. The browser sends the prompt to Odysseus.
2. Odysseus sends an API request through Docker's network.
3. Ollama receives the request.
4. Ollama loads Gemma.
5. Gemma generates tokens.
6. Ollama streams those tokens back to Odysseus.
7. Odysseus displays the response in the browser.

</details>

---

<details>

<summary><strong>❓ If I replace Gemma with Llama, what changes?</strong></summary>

**Answer**

Only the AI model changes.

The browser, Docker, Odysseus, networking, and Ollama remain exactly the same.

One of the advantages of this architecture is that AI models are interchangeable.

</details>

---

<details>

<summary><strong>❓ What is the biggest misconception about this stack?</strong></summary>

**Answer**

Many people believe that Odysseus *is* the AI.

It isn't.

Odysseus is simply the interface.

Ollama is the AI server.

Gemma is the intelligence.

Docker is the infrastructure that allows everything to communicate.

</details>

---

> **Remember**
>
> Think of your AI stack as a team:
>
> - **Browser** → Talks to you.
> - **Odysseus** → Organizes the conversation.
> - **Docker** → Connects everyone together.
> - **Ollama** → Manages the AI models.
> - **Gemma** → Does the actual thinking.
>
> Every component has one job, and together they create a complete locally hosted AI assistant.