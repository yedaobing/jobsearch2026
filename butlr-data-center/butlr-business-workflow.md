# How Butlr Runs Its Business: End-to-End Workflow

## Purpose and scope

This page maps how Butlr turns a thermal sensor and a cloud platform into recurring revenue: how it builds product, sells, deploys, operates, supports, and expands accounts. The data center program workflow owned by the **Senior Program Manager, Data Operations** role is on its own page: [Butlr Data Center Program Workflow](butlr-data-center-program-workflow.md).

Every statement is tagged by where it comes from:

- **Sourced:** stated in the job description or in Butlr's public pages (see [Sources](#sources)).
- **Inferred:** a reasonable reading of how the sourced pieces connect. Confirm these in interviews.

## Butlr at a glance

| Dimension | What Butlr does | Basis |
|---|---|---|
| Mission | Make the built environment "people-aware" while respecting privacy | Sourced (JD) |
| Origin | MIT Media Lab spinout (2019); founders Honghao Deng and Jiani Zeng; offices in Silicon Valley and Boston | Sourced (JD) |
| Core technology | Low-resolution thermal sensing plus AI. Detects presence, counts, traffic, posture, and equipment surface heat without images or PII | Sourced |
| Hardware | Heatic 2+ wireless (multi-year battery), Heatic wired PoE, Heatic Spine rack sensor (USB-C power and data), Hive gateways (Wi-Fi, Ethernet, cellular) | Sourced |
| Software | Intelligence engine (occupancy modeling, traffic, thermal mapping, alerts), Butlr Studio (virtual space setup), apps, APIs and webhooks, Ask Butlr AI analyst | Sourced |
| Applications | Workplace+ (CRE and offices), Butlr Care (fall detection, resident safety), Smart Cleaning (restroom usage), Butlr Data Center (power-path thermal monitoring, thermal digital twin) | Sourced |
| Revenue model | Quote-based hardware plus software subscription; Starter Kit (1 Hive, 3 sensors, 12 months software and API); paid services under SOWs | Sourced (third-party listing and Butlr SOWs) |
| Channels | Direct sales; OEM and embedded (Carrier Abound); co-sell and data partnerships (Disruptive Technologies, GP Pro, Propstack); certified installation partners | Sourced |
| Data center ecosystem | Technology partners Kentec, ASPEED, Cupola360, Provocative | Sourced (DC page) |
| Global operations | Customers in North America, Europe, Asia; a Shenzhen team; customs and import logistics for equipment | Sourced (JD) |
| Investors | Foundry Group, Tiger Global, Qualcomm Ventures, E14 Fund, Carrier, others | Sourced (JD) |

## 1. Business operating model (value chain)

How the parts of the company hand work to each other. The loop at the bottom is what makes it a subscription business: deployed sensors generate data, data proves value, value drives renewal and expansion, and field learnings feed the next product release.

```mermaid
flowchart LR
    subgraph BUILD["Build"]
        A1[Product and R&D<br/>sensors, firmware, AI models, apps]
        A2[Hardware supply chain<br/>Shenzhen team, QA, certification]
    end

    subgraph SELL["Sell"]
        B1[Marketing and demand gen<br/>reports, awards, demos]
        B2[Direct sales<br/>intro call, scoping, proposal]
        B3[Partner channels<br/>OEM, co-sell, installers]
    end

    subgraph DELIVER["Deliver"]
        C1[Order Form and SOW]
        C2[Pilot or POC]
        C3[Deployment<br/>install, configure, commission]
    end

    subgraph OPERATE["Operate and grow"]
        D1[Platform operations<br/>cloud, device health, firmware]
        D2[Customer success<br/>adoption, insight reports, support]
        D3[Renewal and expansion<br/>more floors, sites, modules]
    end

    A1 --> A2
    A1 --> B1
    B1 --> B2
    B1 --> B3
    B2 --> C1
    B3 --> C1
    A2 -->|units shipped| C3
    C1 --> C2
    C2 -->|success criteria met| C3
    C3 --> D1
    D1 --> D2
    D2 --> D3
    D3 -->|expansion order| C1
    D2 -.->|field feedback| A1
    C2 -.->|test results| A1
```

| Function | What it owns | Hands off to | Basis |
|---|---|---|---|
| Product and R&D | Sensor hardware, firmware, intelligence engine, applications, APIs | Supply chain (designs), Marketing (launches) | Sourced (products); handoffs inferred |
| Supply chain and logistics | Configure, test, QA, and ship units; customs and import across borders | Deployment team, POC sites | Sourced (JD) |
| Sales and partners | Discovery, scoping inputs (floor plans, objectives), proposal, Order Form | Delivery (signed scope) | Sourced (sales path); handoff inferred |
| Delivery and installation | Site survey, install, configure zones, commission, closeout report | Platform ops and customer success | Sourced (installation SOW) |
| Platform operations | Device provisioning, firmware, cloud processing, audit and compliance, data pipelines | Customer-facing apps and APIs | Sourced (ecosystem page) |
| Customer success | Adoption, check-ins, issue resolution, insight reports, partner enablement | Sales (expansion), Product (feedback) | Sourced (services list, JD) |

## 2. Platform data flow (what the customer actually buys)

```mermaid
flowchart LR
    S1[Heatic wireless sensors<br/>ceiling, wall, strut, pipe] --> H[Hive gateways<br/>Wi-Fi, Ethernet, cellular]
    S2[Heatic wired PoE and Spine<br/>in-rack, management network] --> H
    S3[Third-party sensors<br/>e.g. Disruptive Technologies] --> CL
    BMC[Server BMC telemetry<br/>utilization, chip temperature] --> CL
    H --> CL[Butlr cloud<br/>provisioning, firmware,<br/>intelligence engine]
    CL --> APP[Applications<br/>Workplace+, Care,<br/>Smart Cleaning, Data Center]
    CL --> API[APIs and webhooks]
    CL --> AL[Alerts<br/>per-zone thresholds]
    API --> EXT[Customer systems<br/>BMS, IWMS, HVAC, booking, custom apps]
    AL --> EXT
    APP --> USER[Facilities, workplace, care,<br/>and data center operators]
```

The hardware is the entry point and the cost of acquisition. The recurring value sits in the cloud layer: analytics, alerts, AI query tools, and integrations into systems the customer already runs. *(Inferred from the hardware plus subscription model.)*

## 3. Customer lifecycle: land, prove, deploy, expand

```mermaid
flowchart TD
    A[Lead: demo request, partner referral,<br/>or OEM channel] --> B[1. Discovery and solution specialist call]
    B --> C[2. Scoping<br/>floor plans, objectives, materials checklist,<br/>sensor layout in Butlr Studio]
    C --> D[3. Proposal and quote<br/>sensors, Hives, subscription, services]
    D --> E{Customer wants<br/>proof first?}
    E -- Yes --> F[4a. Pilot or POC<br/>Starter Kit or scoped pilot]
    F --> G{Success criteria met?}
    G -- No --> G1[Adjust placement, mode,<br/>or use case; retest]
    G1 --> F
    G -- Not viable --> X[Close lost; capture lessons]
    G -- Yes --> H
    E -- No --> H[4b. Order Form signed<br/>plus applicable SOW]
    H --> I[5. Plan and prepare<br/>order and ship hardware,<br/>customer readies power and network]
    I --> J{Site ready one week<br/>before install?}
    J -- No --> J1[Reschedule; change order<br/>if customer-caused delay]
    J1 --> J
    J -- Yes --> K[6. Install and configure<br/>mount sensors, place Hives,<br/>pair devices, create zones]
    K --> L[7. Test and commission<br/>coverage, connectivity, calibration]
    L --> M{Operability verified?}
    M -- No --> M1[Fix placement, network,<br/>or device issue]
    M1 --> L
    M -- Yes --> N[8. Closeout<br/>installation docs, final report]
    N --> O[9. Live operations and customer success<br/>dashboards, alerts, insight reports]
    O --> P{Healthy adoption<br/>and proven value?}
    P -- No --> P1[Resolve issues, retrain,<br/>system modification SOW]
    P1 --> O
    P -- Yes --> Q[10. Renew and expand<br/>more sites, more modules,<br/>long-term contract]
    Q --> C
```

### Stage gates

| Stage | Key activities | Exit gate | Owner | Basis |
|---|---|---|---|---|
| 1. Discovery | Demo tailored to the customer's spaces | Qualified use case and buyer | Sales, solution specialist | Sourced |
| 2. Scoping | Floor plans, objectives, materials checklist, sensor layout and virtual space | Bill of materials and layout | Sales, solutions | Sourced |
| 3. Proposal | Hardware, subscription, services priced | Accepted quote | Sales | Sourced |
| 4a. Pilot / POC | Limited deployment against agreed success criteria | Go / no-go decision | Delivery, engineering | Sourced (pilot program FAQ, JD); criteria inferred |
| 4b. Contract | Order Form plus SOW (installation, system modification, break-fix) | Signed scope | Sales, legal | Sourced (SOWs) |
| 5. Prepare | Ship hardware; customer provides power, network, access, staging space | Site readiness confirmed one week out; install within 60 days of signature | Delivery, customer | Sourced (installation SOW) |
| 6. Install | Mount, connect, configure, pair, zone | Devices online | Butlr or certified installer | Sourced |
| 7. Commission | Functional, connectivity, and calibration tests | Operability verified | Delivery | Sourced |
| 8. Closeout | Documentation and final report | Handoff to operations | Delivery | Sourced |
| 9. Operate | Monitoring, adoption, support, insight reports | Value proven to buyer | Customer success | Sourced (services); gate inferred |
| 10. Expand | More floors, sites, modules (Care, Smart Cleaning, Energy, Data Center) | Expansion order | Customer success, Sales | Inferred |

Butlr states a typical implementation runs **at least 4 weeks**, longer for large or complex sites. Standard on-site installs run on a 4-day work week. *(Sourced.)*

## Business levers and likely metrics (inferred)

| Lever | Why it matters | Metrics to ask about |
|---|---|---|
| Time to value | Subscription revenue starts when sensors produce trusted data | Days from signature to go-live; POC cycle time |
| POC conversion | Data center POCs are expensive; conversion pays for them | POC-to-contract rate; expansion revenue per account |
| Hardware reliability | Battery life and uptime drive support cost and trust | Device online rate; field failure rate; RMA turnaround |
| Logistics | Cross-border shipments can stall a pilot | Ship-to-site lead time; customs hold time |
| Land and expand | Starter Kit lowers entry; value expands by site and module | Net revenue retention; sites and modules per customer |
| Repeatability | Playbooks lower delivery cost per site | Delivery hours per site; repeat issues per deployment |

## Where Dao's background maps

| Butlr need | Matching experience |
|---|---|
| Turn deal commitments into an owned plan | ByteDance three-phase capacity pipeline (demand intake, feasibility workshop, customer validation and delivery) |
| Pilots before configuration decisions | Runs POCs with China partners before settling NPI server configuration |
| Hardware logistics, customs, Shenzhen coordination | Edge PoP builds with equipment import, customs, and compliance; native Mandarin |
| Live data center environments | Edge PoP builds in colocation facilities; Equinix and Digital Realty deliveries; CDCP |
| Environmental and thermal monitoring | Environment monitoring work at Delta and Paylocity |
| Make it repeatable | ByteDance SOP framework built from scratch |
| Gap to address honestly | Post-launch external customer success and account ownership; delivery customers have been internal |

## Questions to confirm in interviews

1. How many data center POCs are active now, and what does a typical one cost and take?
2. What are the written success criteria for converting a data center POC?
3. Is the CFD comparison a standard validation step or customer-specific?
4. Where are units built and configured, and who owns customs and import today?
5. How is the data center offering priced: per rack, per MW, per sensor, or per site?
6. Who owns the account after expansion: this role, Sales, or a CSM?

## Sources

- Butlr, *Senior Program Manager, Data Operations* job description (BambooHR, accessed 29 Oct 2026)
- [Butlr Data Center solution](https://www.butlr.com/solutions/data-center)
- [How Butlr addresses the data center energy efficiency challenge](https://www.butlr.com/blog/how-butlr-addresses-the-data-center-energy-efficiency-challenge)
- [Butlr platform overview (support)](https://support.butlr.io/hc/en-us/articles/33781555446285)
- [Understanding the Butlr Ecosystem](https://support.butlr.io/hc/en-us/articles/46194494315533-Understanding-the-Butlr-Ecosystem)
- [What products and services does Butlr offer?](https://support.butlr.io/hc/en-us/articles/41507309145869-What-products-and-services-does-Butlr-offer)
- [What is the installation process like?](https://support.butlr.io/hc/en-us/articles/41507836020621-What-is-the-installation-process-like)
- [What is the typical implementation timeline?](https://support.butlr.io/hc/en-us/articles/41507809914637-What-is-the-typical-implementation-timeline)
- [Workplace: On-Site Installation SOW](https://www.butlr.com/statements-of-work/workplace-on-site-installation)
- [Butlr Workplace pricing summary (FitGap)](https://us.fitgap.com/products/029786/butlr-workplace)
- [Butlr and Disruptive Technologies partnership (Business Wire, Mar 2026)](https://www.businesswire.com/news/home/20260312111938/en/)
- [Butlr's new thermal sensor products (Commercial Observer, Sep 2026)](https://commercialobserver.com/2026/09/butlr-new-thermal-sensor-products/)
- [Butlr Technologies (Wikipedia)](https://en.wikipedia.org/wiki/Butlr_Technologies)

## Source boundary and assumptions

Butlr does not publish its internal org chart, pricing, POC success criteria, manufacturing locations beyond the JD's mention of a Shenzhen team, or data center customer names. Data center payback figures on Butlr's site are company-modeled, not realized results, and are left out of this workflow. Handoffs between functions, stage-gate evidence, and the metrics table are inferred and should be validated with the hiring team.
