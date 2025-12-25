# Contributing to OpenEV Data

Thank you for your interest in contributing to OpenEV Data! This project aims to be the single source of truth for electric vehicle specifications, and we welcome contributions from EV enthusiasts, engineers, researchers, and manufacturers worldwide.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Repository Structure](#repository-structure)
- [Contributing to the Dataset](#contributing-to-the-dataset)
- [Contributing to the API](#contributing-to-the-api)
- [Contributing to Documentation](#contributing-to-documentation)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
- [Data Quality Standards](#data-quality-standards)

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

If you find a bug, please create an issue using the bug report template. Include:

- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Screenshots if applicable

### Suggesting Features

Feature suggestions are welcome via the feature request template. Please:

- Clearly describe the feature and its use case
- Explain why it would be valuable to the community
- Consider implementation complexity

### Correcting Vehicle Data

Data accuracy is our top priority. If you find incorrect vehicle specifications:

- Use the data correction issue template
- Provide reliable sources for the correction
- Specify which field(s) are incorrect and the correct values

### Adding New Vehicles

To add a new vehicle to the dataset:

- Use the new vehicle issue template first to discuss
- Follow the schema structure in `open-ev-data-dataset`
- Provide multiple reliable sources for all specifications

## Repository Structure

OpenEV Data consists of four repositories:

| Repository | Purpose | Primary Language |
|:-----------|:--------|:-----------------|
| [open-ev-data-dataset](https://github.com/open-ev-data/open-ev-data-dataset) | Vehicle data and JSON schemas | JSON |
| [open-ev-data-api](https://github.com/open-ev-data/open-ev-data-api) | API engine and ETL pipeline | Rust |
| [open-ev-data.github.io](https://github.com/open-ev-data/open-ev-data.github.io) | Documentation website | MkDocs |
| [.github](https://github.com/open-ev-data/.github) | Governance and policies | Markdown |

## Contributing to the Dataset

### Prerequisites

- Node.js 18+ installed
- Understanding of JSON Schema
- Familiarity with vehicle specifications

### Setup

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
cd open-ev-data-dataset
npm install
```

### Adding a Vehicle

1. Read the [Schema Documentation](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/SCHEMA.md)
2. Read the [Architecture Documentation](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/ARCHITECTURE.md)
3. Create the vehicle directory structure:

```
src/
└── manufacturer_slug/
    └── model_slug/
        ├── base.json
        └── year/
            └── trim.json
```

4. Create `base.json` with specifications common to all years and trims
5. Create year-specific files with year-specific changes
6. Follow the deep merge architecture

### Data Requirements

All vehicle entries must include:

- **Verified Sources**: Minimum of 2 reliable sources per specification
- **International Coverage**: Include sources from USA, Brazil, EU (Portugal, Germany, France, Italy, UK), China, and Japan where applicable
- **Complete Specifications**: Battery capacity, range, charging specs, dimensions, performance
- **Correct Units**: Follow SI units as defined in the schema
- **Charging Standards**: Accurate connector types and charging curves

### Validation

Before submitting:

```bash
npm run validate
```

Fix any schema validation errors before creating a pull request.

### Source Quality Hierarchy

1. Official manufacturer specifications
2. Regulatory certifications (EPA, WLTP, CLTC)
3. Professional automotive publications
4. Verified user testing data

Avoid:
- Unverified forums or social media
- Estimations without clear methodology
- Outdated sources

## Contributing to the API

### Prerequisites

- Rust 1.75+ installed via rustup
- Understanding of REST APIs
- Familiarity with WebAssembly (for edge deployments)

### Setup

```bash
git clone https://github.com/open-ev-data/open-ev-data-api.git
cd open-ev-data-api
cargo build
cargo test
```

### Development Guidelines

- Follow Rust idioms and best practices
- Write comprehensive tests for new features
- Ensure zero-panic code in production paths
- Document public APIs with rustdoc
- Run `cargo clippy` before committing
- Format code with `cargo fmt`

### Performance Considerations

- API targets <50ms response times globally
- Optimize for edge runtime constraints
- Consider SQLite query performance
- Minimize WASM binary size

## Contributing to Documentation

### Prerequisites

- Python 3.9+ installed
- MkDocs Material familiarity

### Setup

```bash
git clone https://github.com/open-ev-data/open-ev-data.github.io.git
cd open-ev-data.github.io
```

Follow the website repository README for complete setup instructions.

### Documentation Standards

- Use clear, concise language
- Include code examples where applicable
- Test all commands and code snippets
- Follow DRY principles by referencing other docs instead of duplicating
- Maintain consistent formatting
- Update navigation when adding new pages

## Pull Request Process

### Before Submitting

1. **Fork** the repository
2. **Create a branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** following the style guidelines
4. **Test thoroughly**:
   - Dataset: Run `npm run validate`
   - API: Run `cargo test` and `cargo clippy`
   - Docs: Build and preview locally
5. **Commit with clear messages**:
   ```bash
   git commit -m "Add: descriptive message about changes"
   ```
6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

### Submitting the PR

1. Go to the original repository
2. Click "New Pull Request"
3. Select your branch
4. Fill out the pull request template completely
5. Link related issues using keywords (Fixes #123, Closes #456)
6. Wait for review

### Review Process

- Maintainers will review within 7 days
- Address requested changes promptly
- Keep discussions focused and professional
- Be open to feedback and suggestions

### After Approval

- Squash commits if requested
- Maintainers will merge your PR
- Your contribution will be included in the next release

## Style Guidelines

### General

- Use English for all code, comments, and documentation
- Follow SOLID principles for code architecture
- Apply DRY principles to avoid duplication
- Avoid unnecessary comments; code should be self-documenting
- Do not use emojis in code or data files

### Git Commits

Follow conventional commit format:

```
<type>: <description>

[optional body]

[optional footer]
```

Types:
- `Add`: New feature or data
- `Fix`: Bug fix
- `Update`: Modification to existing feature/data
- `Remove`: Deletion of feature or data
- `Docs`: Documentation changes
- `Refactor`: Code refactoring
- `Test`: Test additions or modifications
- `Chore`: Maintenance tasks

### JSON Formatting (Dataset)

- Use 2-space indentation
- Sort keys alphabetically where logical
- Use double quotes for strings
- Include trailing commas in arrays and objects
- Validate against schema before committing

### Rust Code (API)

- Follow Rust naming conventions
- Use `cargo fmt` default configuration
- Maximum line length: 100 characters
- Prefer explicit types in public APIs
- Use Result types for error handling

## Data Quality Standards

### Accuracy

- All specifications must be verified against reliable sources
- When sources conflict, prioritize official manufacturer data
- Document assumptions clearly in source notes
- Update data when new information becomes available

### Completeness

Each vehicle entry should include:
- Battery specifications (capacity, chemistry, voltage)
- Range data (WLTP, EPA, CLTC where available)
- Charging specifications (AC and DC with curves)
- Performance metrics (acceleration, top speed)
- Physical dimensions and weight
- Market availability by country

### International Standards

- Include regional variations where specifications differ
- Document charging standards by market
- Provide sources from multiple regions
- Note regulatory differences (EPA vs WLTP)

### Versioning

- Use manufacturer model years
- Document mid-cycle updates as separate variants
- Track specification changes over time
- Maintain backward compatibility in data structure

## Questions?

- Check existing [issues](https://github.com/open-ev-data/.github/issues)
- Review [documentation](https://open-ev-data.github.io)
- Start a [discussion](https://github.com/orgs/open-ev-data/discussions)

## License

By contributing, you agree that your contributions will be licensed under:
- **Dataset**: CDLA-Permissive-2.0
- **API/Code**: Apache License 2.0
- **Documentation**: CC-BY 4.0

See the LICENSE file in each repository for details.

---

Thank you for helping make OpenEV Data the most accurate and comprehensive EV specification database!

