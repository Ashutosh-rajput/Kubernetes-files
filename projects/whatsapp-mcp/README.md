# 📱 WhatsApp MCP – Modular Command Processor for WhatsApp Automation

This project provides a Kubernetes-deployable server for interacting with WhatsApp using SSE (Server-Sent Events). The WhatsApp MCP can automate and control nearly any WhatsApp task programmatically via a set of powerful tools.

---

## 🚀 Features

The WhatsApp MCP supports the following tools:

- `search_contacts`: Search through contacts
- `list_messages`: Retrieve message history
- `list_chats`: List all existing chats
- `get_chat`: Get detailed info on a specific chat
- `get_direct_chat_by_contact`: Open chat with a specific contact
- `get_contact_chats`: Retrieve all chats linked to a contact
- `get_last_interaction`: Get the most recent interaction with a user
- `get_message_context`: Retrieve message context
- `send_message`: Send plain text messages
- `send_file`: Send documents or images
- `send_audio_message`: Send audio clips
- `download_media`: Download media from received messages

---

## ⚙️ Deployment Instructions

To deploy the WhatsApp MCP on **Kubernetes**, apply the following YAML files:

```bash
kubectl apply -f whatsapp-pvc.yaml
kubectl apply -f whatsapp-server.yaml
```

### 📍 Accessing the Server

- **Locally**:  
  If you're running Docker Desktop with Kubernetes enabled, access it at:  
  `http://localhost:8082/sse`

- **On GCP / AWS or Cloud Kubernetes**:  
  Get the external IP address of the service:
  ```bash
  kubectl get svc whatsapp-service
  ```
  Then access:
  ```
  http://<external-ip>:8082/sse
  ```

---

## 💡 Usage

The WhatsApp MCP uses **Server-Sent Events (SSE)** to stream data. You can integrate it with any **SSE-compatible MCP client**.

> 🔍 Check the `client/` folder for:
> - DeepSeek-based client implementation
> - OpenAI-based client setup

These clients provide LLM-powered automation via your WhatsApp MCP interface.


## ✅ Prerequisites

- Kubernetes cluster (local or cloud)
- Docker Desktop (if running locally)
- kubectl configured for your cluster
- (Optional) DeepSeek/OpenAI credentials for LLM-enhanced automation

---

## 🧠 Tip

Use this project as a backbone to build intelligent, event-driven WhatsApp bots, agents, or integrations for CRMs, customer service, or personal assistants.

---

## 📜 License

MIT License. Feel free to use and modify as per your needs.

---

> 👤 Author: Ashutosh Rajput  
> 🌐 Project: [WhatsApp-MCP](#)
