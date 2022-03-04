# Animalscape

Learn AWS by solving scenrio!

## Overview

- Animal Rescue and Awareness Organization
- `Global`,` with HQ in Brisbane, Korea - `100` members
- ...Call Center, Admin, IT, Marketing, Legal & Accounts
- `~100` Remote workers across Korea and Globally
- ... Animal care, activists & Lobbyists
- Major Offices in `London, New York & Seattle`

## Current technical infrastructure

- Small `on-premises` datacenter in `Brisbane`
- Datacenter is old and manager wants to migrate to AWS.
- Badly Implemented AWS trial in `Sydney` Region. (no resilience and scalability)
- A few isolated Azure/GCP Pilots
- Global Offices & mobile staff utilize Seoul Infrastructure
- `Cost-conscious` but `progressive` management team.

## Global Architecture

The business has three non-Australian major offices. One is London, covertin the EU rgion, and then ast and West Coast U.S., specifically New York and Settle. 

These remote offices currently consume the IT serivices provided by the Brisbane had office, which has proven to be less than ideal from a performance perspective.

Animalscape emply a large group of field workers, who have varid skill sets and job roles. Some of them aree working on IOT projects, machine learning, or doing big data projects out in the field.

They carry various bits of equipment, including a rugged laptop with 3G, 4G, or satelite connectivity, they need to upload and download data, which ranges in size and complexity, and vice versa. Whatever implemenatations they are, we need to support the working activity of these workers.

Therefore, Animalscape platform needs to be available around the clock. 

## Current Problems

- Legacy on-premises hadrware is `failing` (expected to be decommissioned in 18 months)
- AWS/Azure Pilots are `messy` and `not best practice`
- Performance issues for filed workers because of their distance
- Lack of HA and Scability - hardware is expensive
- Staff skills/capabilities struggle... `little automation`
- Global expansion concerns - `cost for new infrastructure`

## Ideal Outcomes

- Fast performance for all field workers
- Able to deploy into `new regions quickly` when required
- Low cost & scalable base infrastructure
- `Agility` - spin up new marketing campaigns, social and progressive applications (`IOT, Big Data` etc)
- `Automation` - low base staffing costs