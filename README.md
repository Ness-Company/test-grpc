# test-grpc

Proof of Concept demonstrating gRPC-based communication between internal microservices.

## Overview

This repository was created to evaluate whether gRPC is a suitable replacement for REST APIs for internal service-to-service communication within the Ness trading platform.

The project demonstrates:

- Defining APIs with Protocol Buffers
- Generating Python gRPC clients and servers
- Communication between independent services
- Integrating a Django application with a gRPC backend
- Sharing protobuf contracts across services

The goal is not to provide production-ready code, but to validate the architecture and developer experience.

---

## Architecture

```
                  +-------------------+
                  |  Protocol Buffers |
                  |  something.proto  |
                  +---------+---------+
                            |
            +---------------+---------------+
            |                               |
     Generate Server                 Generate Client
            |                               |
            v                               v
+-------------------------+        +-------------------------+
|      service_b          |        |      service_a          |
|                         |        |                         |
| gRPC Server             | <----> | Django Application      |
| Business Logic          |        | gRPC Client             |
+-------------------------+        +-------------------------+
```

---

## Project Structure

```
.
├── protos/
│   └── something.proto
│
├── service_a/
│   ├── Django application
│   └── Generated gRPC client
│
├── service_b/
│   ├── gRPC server
│   └── Generated protobuf code
│
└── requirements.txt
```

---

## Objectives

This PoC evaluates:

- gRPC performance compared to REST
- Type-safe communication
- Developer workflow
- Protocol Buffer code generation
- Integration with existing Django services
- Feasibility for microservice architecture

---

## Workflow

1. Define the service contract in `something.proto`
2. Generate Python bindings
3. Implement the server
4. Consume the service from another application

```
.proto
    ↓
Generate Python Code
    ↓
Server Implementation
    ↓
Client Implementation
    ↓
RPC Communication
```

---

## Running the Example

### Install dependencies

```bash
pip install -r requirements.txt
```

### Start the gRPC server

```bash
python service_b/server.py
```

### Run the Django application

```bash
cd service_a

python manage.py runserver
```

The Django application communicates with the gRPC server using the generated client.

---

## Why gRPC?

Compared to REST APIs, gRPC provides:

- HTTP/2 transport
- Strongly typed contracts
- Automatic client generation
- Smaller binary payloads
- Streaming support
- Lower latency
- Better fit for internal microservice communication

---

## Status

**Proof of Concept**

This repository exists to validate the architecture before introducing gRPC into production services within the Ness trading platform.
