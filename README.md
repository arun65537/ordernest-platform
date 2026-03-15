# OrderNest Platform

OrderNest is a microservices-based e-commerce platform.  
This repository is the parent repository that links all service repositories using Git submodules.

Homepage: https://ordernest-web.onrender.com

## Repositories in This Platform

- `ordernest-auth-service` - JWT authentication and user identity
- `ordernest-inventory-service` - product catalog and stock management
- `ordernest-order-service` - order creation and order lifecycle
- `ordernest-payment-service` - payment processing (Razorpay) and payment events
- `ordernest-shipment-service` - shipment status updates and shipment events
- `ordernest-web` - React frontend (Vite + Tailwind)

## Architecture Overview

- Frontend (`ordernest-web`) calls auth, inventory, and order APIs.
- Backend services are Spring Boot services (Java 17, Gradle).
- PostgreSQL is used for persistence in core services.
- Kafka is used for event-driven communication (payment/shipment related events).

## Why This Parent Repo Uses Submodules

This repo gives one top-level project for coordination while preserving:

- independent history per service
- independent deployments per service
- clear version pinning across services for stable releases

## Clone and Initialize

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/arunsingh8775/ordernest-platform.git
```

If already cloned without submodules:

```bash
git submodule update --init --recursive
```

## Pull Latest Changes

To pull parent repo updates and refresh submodules:

```bash
git pull
git submodule update --init --recursive
```

To move each submodule to the latest commit on its default branch:

```bash
git submodule update --remote --recursive
```

Then commit updated submodule pointers in this parent repo:

```bash
git add .
git commit -m "Update submodule pointers"
git push
```

## Local Development (Suggested Flow)

1. Start required infrastructure (PostgreSQL, Kafka) for backend services.
2. Start backend services one by one from their directories.
3. Start frontend:

```bash
cd ordernest-web
npm install
npm run dev
```

Each service has its own detailed setup and environment variables in its own `README.md`.

## Working in a Specific Service

Example (`ordernest-order-service`):

```bash
cd ordernest-order-service
git checkout master
# make changes
git add .
git commit -m "Your change"
git push
```

After that, return to parent repo and update the submodule pointer:

```bash
cd ..
git add ordernest-order-service
git commit -m "Bump order-service submodule"
git push
```

## Service Docs

- [Auth Service](./ordernest-auth-service/README.md)
- [Inventory Service](./ordernest-inventory-service/README.md)
- [Order Service](./ordernest-order-service/README.md)
- [Payment Service](./ordernest-payment-service/README.md)
- [Shipment Service](./ordernest-shipment-service/README.md)
- [Web Frontend](./ordernest-web/README.md)
