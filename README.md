# Multi-Tenant-Comerce
The Multi-tenant Commerce allows merchants to create and operate isolated online stores. Store owners and staff manage products, inventory, customers, and orders, while end customers browse storefronts and place purchases. The platform integrates with external payment, email, and object-storage providers.

## System Architecture Diagram

The following structure represents the flow and relationships.

```mermaid
flowchart TD
    %% Styling Conventions
    classDef coreSystem fill:#1168bd,stroke:#0b4884,color:#ffffff,rx:8px,ry:8px,stroke-width:2px
    classDef actor fill:#08427b,stroke:#052e56,color:#ffffff,rx:4px,ry:4px
    classDef externalSystem fill:#999999,stroke:#666666,color:#ffffff,rx:4px,ry:4px

    %% Human Actors (Top Level)
    Owner["Store Owner"]:::actor
    Staff["Store Staff"]:::actor
    Customer["End Customer"]:::actor
    Admin["Platform Admin"]:::actor

    %% Core System (Middle Level)
    SaaS["Multi-tenant Commerce.    "]:::coreSystem

    %% External Systems (Bottom Level)
    Payment["Payment Gateway"]:::externalSystem
    Email["Email Provider"]:::externalSystem
    Storage["Object Storage"]:::externalSystem
    Shipping["Shipping Provider"]:::externalSystem

    %% Interactions: Actors -> Core System
    Owner -- "Creates stores, manages<br/>catalog, team, and billing" --> SaaS
    Staff -- "Manages products,<br/>inventory, and orders" --> SaaS
    Customer -- "Browses products, creates<br/>carts, and places orders" --> SaaS
    Admin -- "Manages tenants, plans,<br/>and platform support" --> SaaS

    %% Interactions: Core System -> External Systems
    SaaS -- "Creates payment sessions<br/>and receives webhooks" --> Payment
    SaaS -- "Sends invitations, receipts,<br/>and notifications" --> Email
    SaaS -- "Stores product images and<br/>exports" --> Storage
    SaaS -- "Creates shipments and<br/>receives delivery updates" --> Shipping
