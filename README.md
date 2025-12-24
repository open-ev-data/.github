# OpenEV Data

![OpenEV Data Logo](./assets/open-ev-data.svg)

> **The Single Source of Truth for Electric Vehicle Specifications.**

The primary goal of **OpenEV Data** is to develop and maintain the world's most accurate, scientifically validated, and accessible open database of Electric Vehicle (EV) specifications. Unlike fragmented proprietary lists, OpenEV is built on **Data-as-Code** principles, ensuring version control, strict schema validation, and community review for every data point—from battery chemistry to charging curves.

Our infrastructure is powered by a high-performance **Rust** ecosystem. The API runs on the Edge (WebAssembly), providing global low-latency access to data, while the dataset itself is agnostic and available for direct download in JSON or SQL formats.

We aim to speed up eMobility adoption by providing developers, researchers, and charging network operators with a reliable standard (The "OpenEV Spec") to build better routing algorithms, chargers, and apps.

## Repository Structure

OpenEV Data is modular by design to separate concerns between data curation and software engineering.

| Repository | Description | Tech Stack |
| :--- | :--- | :--- |
| [**open-ev-data-dataset**](https://github.com/open-ev-data/open-ev-data-dataset) | The core database. Contains all vehicle JSONs and validation schemas. | JSON, JSON Schema |
| [**open-ev-data-api**](https://github.com/open-ev-data/open-ev-data-api) | The high-performance engine. Handles ETL, SQL generation, and the Edge API. | **Rust**, Wasm, Cloudflare Workers |
| [**open-ev-data.github.io**](https://github.com/open-ev-data/open-ev-data.github.io) | Official documentation, guides, and API reference. | MkDocs, Material |
| [**.github**](https://github.com/open-ev-data/.github) | Governance, organization-wide policies, and issue templates. | Markdown |

## Getting Started

To start consuming the data or contributing to the project, please read our [**Documentation**](https://open-ev-data.github.io).

- **For Data Scientists:** Clone [open-ev-data-dataset](https://github.com/open-ev-data/open-ev-data-dataset) to access raw JSON files.
- **For Developers:** Check the [API Reference](https://open-ev-data.github.io/api) to integrate OpenEV into your app.

## Project Status

- **Website:** [open-ev-data.github.io](https://open-ev-data.github.io)
- **API Status:** [![Status](https://img.shields.io/website?url=https%3A%2F%2Fapi.open-ev-data.org%2Fhealth)](https://github.com/open-ev-data/open-ev-data-api)
- **Data Version:** [![Latest Release](https://img.shields.io/github/v/release/open-ev-data/open-ev-data-dataset)](https://github.com/open-ev-data/open-ev-data-dataset/releases)

### Technical Overview

- **Strict Typing:** All data is validated against rigorous JSON Schemas (`vehicle.schema.json`) before merging.
- **Deep Merge Architecture:** Uses a hierarchical inheritance model (Base -> Year -> Trim) to ensure DRY (Don't Repeat Yourself) data entry.
- **Edge Computing:** The API is deployed globally using Cloudflare Workers and D1 (SQLite), ensuring <50ms latency.
- **Rust Core:** All tooling (ETL, Validation, Server) is written in Rust for safety and performance.

### Roadmap

See our technical roadmap on our [project website](https://open-ev-data.github.io/roadmap/).

### Supported Standards
OpenEV Data standardizes specifications across multiple global charging standards:

- **CCS2** (EU/Global)
- **NACS / J3400** (North America/Tesla)
- **CCS1** (North America Legacy)
- **GB/T** (China)
- **CHAdeMO** (Japan/Legacy)
- **Type 2 / Type 1** (AC Charging)

## Contributing

We welcome contributions from EV enthusiasts, engineers, and manufacturers. Precision is our priority.

- **To add a vehicle:** Please open a Pull Request in the `open-ev-data-dataset` repository using the provided templates.
- **To improve the API:** Please check the issues in the `open-ev-data-api` repository.

Read our [Contribution Guidelines] before submitting.

## Governance & Licensing

This project employs a dual-licensing strategy to best serve the ecosystem:

1.  **Software (API/CLI):** Licensed under the **Apache License, Version 2.0**. Safe for enterprise integration and patent protection.
2.  **Database (Dataset):** Licensed under the **CDLA-Permissive-2.0** (Community Data License Agreement). Optimized for open data sharing and mining.
3.  **Documentation:** Licensed under **CC-BY 4.0**.

See [LICENSE](LICENSE) in each repository for specific details.

## Support

If you identify a data error or a bug in the API, please [open an issue](https://github.com/open-ev-data/.github/issues) using the appropriate template.

---

[Contribution Guidelines]: CONTRIBUTING.md