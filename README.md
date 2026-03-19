# OrderNest Platform

OrderNest is a microservices-based e-commerce platform.  
This repository is the parent workspace that links all services through Git submodules.

Live App: [https://ordernest-web.onrender.com](https://ordernest-web.onrender.com)

## Stack

- Backend: Java 17, Spring Boot, Gradle
- Frontend: React, Vite, Tailwind CSS
- Database: PostgreSQL
- Messaging: Kafka
- Payments: Razorpay (test mode integration)

## Services

| Service | Responsibility | Docs |
| --- | --- | --- |
| `ordernest-auth-service` | JWT auth, registration, login, user identity | [README](./ordernest-auth-service/README.md) |
| `ordernest-inventory-service` | Product catalog, stock, inventory APIs | [README](./ordernest-inventory-service/README.md) |
| `ordernest-order-service` | Order creation, lifecycle, and shipment status workflow | [README](./ordernest-order-service/README.md) |
| `ordernest-payment-service` | Razorpay order/payment verification and payment events | [README](./ordernest-payment-service/README.md) |
| `ordernest-web` | Customer-facing React frontend | [README](./ordernest-web/README.md) |

## Quick Start

Clone with all submodules:

```bash
git clone --recurse-submodules https://github.com/arun65537/ordernest-platform.git
cd ordernest-platform
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

## Run Locally

1. Start required infrastructure (PostgreSQL and Kafka).
2. Start backend services from their respective folders.
3. Start frontend:

```bash
cd ordernest-web
npm install
npm run dev
```

## Submodule Workflow

Update parent + pinned service versions:

```bash
git pull
git submodule update --init --recursive
```

Pull latest commits from service default branches:

```bash
git submodule update --remote --recursive
git add .
git commit -m "Update submodule pointers"
git push
```

Make changes in one service:

```bash
cd ordernest-order-service
git checkout master
# make changes
git add .
git commit -m "Your change"
git push
```

Then update parent pointer:

```bash
cd ..
git add ordernest-order-service
git commit -m "Bump order-service submodule"
git push
```

## Why This Repo Exists

- Single top-level workspace for all services
- Independent history and deployment per service
- Stable cross-service version pinning for releases
