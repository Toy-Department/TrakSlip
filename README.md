# TrakSlip | Construction Time & Material Tracking Software

![License](https://img.shields.io/badge/license-Private-red)
![Status](https://img.shields.io/badge/status-Production-success)
![Stack](https://img.shields.io/badge/stack-Next.js_16_Supabase_Stripe-blue)

**Eliminate paper T&M tickets. The digital standard for General Contractors and Subcontractors to track time, materials, and approvals.**
www.trakslip.com

---

## 🚀 The Why
**Problem**: Verification of Extra Work, Time & Materials (T&M) is chaos. Construction projects lose thousands in revenue due to lost, illegible, disputed paper tickets or fraud. Admin teams waste hours manually typing extensive handwritten logs into invoices and tracking uncompleted work.

**Solution**: TrakSlip digitizes the entire workflow. 
1. **Field Verification**: Subcontractors log hours and materials instantly on mobile.
2. **Real-Time Approval**: General Contractors review and sign digitally on the spot.
3. **Instant Invoicing**: Validated PDF reports are generated instantly, speeding up payment cycles by 40%.

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: ![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat&logo=next.js&logoColor=white) (App Router)
- **Language**: ![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)
- **Styling**: ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
- **State**: React Context (Auth, Toast, PostHog)
- **Analytics**: ![PostHog](https://img.shields.io/badge/PostHog-black?style=flat&logo=posthog&logoColor=white)

### Backend (Serverless)
- **Platform**: ![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white) (Edge Network)
- **Database**: ![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white) (PostgreSQL)
- **Auth**: Supabase Auth
- **Realtime**: Supabase Realtime (WebSockets)

### Integrations
- **Payments**: ![Stripe](https://img.shields.io/badge/Stripe-008CDD?style=flat&logo=stripe&logoColor=white)
- **Email**: ![Resend](https://img.shields.io/badge/Resend-black?style=flat&logo=resend&logoColor=white)

---

## 🏗️ Architecture

TrakSlip leverages an Event-Driven, Edge-First architecture to ensure speed on job sites and strict data isolation between competing contractors.

```mermaid
graph LR
    User([User])
    
    subgraph Frontend [Next.js App Router]
        UI[Pages / Components]
        State[State Management]
    end
    
    subgraph Backend [Supabase & Edge]
        API[API Routes]
        DB[(Postgres DB)]
        Realtime[Realtime Engines]
    end
    
    subgraph External [Integrations]
        Stripe[Stripe]
        Resend[Resend]
    end

    %% Key Flows
    User -->|HTTPS| UI
    UI <-->|Direct Data| DB
    UI -->|Server Actions| API
    
    API -->|Webhooks| Stripe
    API -->|Emails| Resend
    
    %% Realtime Flow
    DB -.->|CDC| Realtime
    Realtime -.->|WebSockets| User
    
    %% Styles
    style UI fill:#000,stroke:#fff,color:#fff
    style DB fill:#3ECF8E,stroke:#333,color:#fff
    style Stripe fill:#635BFF,stroke:#fff,color:#fff
```

### Key Architectural Highlights
*   **Row Level Security (RLS)**: We don't just filter data in the API. Security policies are enforced directly in the database engine, ensuring a Subcontractor can *never* access another company's data, even if the API layer fails.
*   **Real-Time Sync**: When a ticket status changes from "Pending" to "Approved", the UI updates instantly for all connected users without a page reload, powered by Postgres CDC and WebSockets.
*   **Edge Functions**: Critical logic runs on Vercel's Edge Network, reducing latency for mobile users on cellular data.

---

## ✨ Key Features

### 🏗️ Digital T&M Workflow
*   **Instant Digital Tickets**: Mobile-friendly forms optimized for entry in the field.
*   **Digital Signatures**: Capture authentic signatures from GCs on-site (touchscreen).
*   **Photo Evidence**: Mandatory photo upload steps to reduce disputes (e.g., "Show me the damaged conduit").
*   **Contextual Messaging**: Dedicated chat threads on every ticket allow GCs and Subs to resolve questions instantly without chasing emails.

### 🏢 Organization & Management
*   **Role-Based Portals**:
    *   **General Contractor**: Dashboard for approvals, disputes, and project oversight.
    *   **Subcontractor**: Field-focused interface for quick entry and status tracking.
*   **Inventory Control**: Define standard materials and personnel rates (e.g., "Journeyman - $85/hr") to prevent billing errors.

### 🚀 Productivity
*   **One-Click Invoicing**: Generate professional, branded PDF reports ready for billing with `jsPDF`.
*   **Anti-Fraud Ledger**: A permanent, non-editable audit log of every action (Created, Edited, Viewed, Approved). Actions cannot be hidden or deleted without a trace.

---

## 📸 Visuals

| Landing Page | Ticket Entry (Mobile) |
|:---:|:---:|
| <img width="564" height="308" alt="image" src="https://github.com/user-attachments/assets/5703fe6f-b9f9-402e-a7a0-8e287bb0b328" /> | <img width="201" height="305" alt="image" src="https://github.com/user-attachments/assets/1bd730c8-9828-4004-948a-d40fb838fbd4" /> |

| GC Dashboard | SC Dashboard |
|:---:|:---:|
| <img width="564" height="308" alt="image" src="https://github.com/user-attachments/assets/7394c079-db29-4788-841f-2817e8882975" /> | <img width="564" height="308" alt="image" src="https://github.com/user-attachments/assets/73a0c738-2eaf-4b8a-83f5-4252dfec13da" /> |

---

## 📄 License
This project is proprietary and confidential. Unauthorized copying of this file, via any medium is strictly prohibited.









## ⚠️ Note on Deployment

**This repository contains the source code for TrakSlip. The code is not currently published or deployed from this public repository due to security considerations and ongoing development.**

We are sharing this README to showcase the architecture and technologies used in building this application.
