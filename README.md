# MVP-Kit

MVP-Kit is a practical guide and toolkit for building MVP (Minimum Viable Product) infrastructure using open-source tools.

This project is a reflection of my hands-on experience as a non-developer navigating the technical requirements of building and deploying MVPs.

Key Goals:

- Speed and Efficiency: Avoid reinventing the wheel by using prebuilt solutions for repetitive tasks.
- Cost-Effectiveness: Explore self-hosted solutions to manage infrastructure costs.
- Practicality: Learn from real-world experience and trial-and-error rather than purely technical documentation.

This repository accompanies a series of posts titled "Building MVP Infrastructure with Open Source Tools."

Refer to this series for explanations on why this repository was created, the rationale behind specific decisions, the advantages of these choices, and their potential limitations. It provides a guide to understanding the trade-offs and benefits of using open-source tools for building MVP infrastructure, along with practical examples and insights.

## Important Considerations

A few key points to keep in mind:

- This repository isn't meant to be a production deployment guide
- Security isn't covered in depth - additional measures would be needed for production
- Open source tools come with their own challenges (maintenance, potential abandonment, slower updates)
- Supporting open source projects through paid tiers or contributions is highly encouraged

## Core Open Source Tools

The MVP-Kit leverages the following tools to build a robust infrastructure:

- [Supabase](https://supabase.com/): Backend server with REST APIs
- [Directus](https://directus.io/): Headless CMS
- [Jitsu](https://jitsu.com/): Data ingestion engine
- [Airbyte](https://airbyte.com/): Data integration platform
- [Mage.ai](https://www.mage.ai/): Workflows for data engineering
- [n8n](https://n8n.io/): Workflow automation software
- [Metabase](https://www.metabase.com/): Business intelligence, dashboards, and data visualization
- [Chatwoot](https://www.chatwoot.com/): Customer engagement platform
- [Typebot](https://typebot.io/): Conversational apps builder

## Getting Started

1. [Initial Server Setup and Proxmox Installation](./instructions/docs/server-proxmox-setup.md)

2. [Setting Up VMs with Portainer and Traefik](./instructions/docs/traefik-portainer-setup.md)
