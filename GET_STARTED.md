# Getting Started with OpenEV Data Development

This guide will walk you through setting up the complete OpenEV Data development environment by cloning all repositories and configuring your workspace for efficient cross-repository development.

## Prerequisites

- [Git](https://git-scm.com/)
- [Visual Studio Code](https://code.visualstudio.com/) or [Cursor](https://cursor.sh/)
- [Node.js](https://nodejs.org/) (for dataset validation)
- [Rust](https://www.rust-lang.org/) (for API development)

## Repository Structure

OpenEV Data consists of four interconnected repositories:

| Repository | Purpose |
|:-----------|:--------|
| `open-ev-data-dataset` | Core vehicle database with JSON files and schemas |
| `open-ev-data-api` | Rust-based API and ETL pipeline |
| `open-ev-data.github.io` | Documentation website |
| `.github` | Governance, policies, and organization-wide templates |

## Installation

### Step 1: Create Project Root Directory

Create a parent directory to hold all repositories:

```bash
mkdir open-ev-data
cd open-ev-data
```

### Step 2: Clone All Repositories

Clone each repository into the parent directory:

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
git clone https://github.com/open-ev-data/open-ev-data-api.git
git clone https://github.com/open-ev-data/open-ev-data.github.io.git
git clone https://github.com/open-ev-data/.github.git
```

Your directory structure should now look like this:

```
open-ev-data/
├── open-ev-data-dataset/
├── open-ev-data-api/
├── open-ev-data.github.io/
└── .github/
```

### Step 3: Open the Multi-Repository Workspace

The `.github` repository contains a pre-configured workspace file that allows you to work with all repositories simultaneously.

#### Using Visual Studio Code or Cursor:

**Option A: Command Line**
```bash
code .github/open-ev-data.code-workspace
```

Or if using Cursor:
```bash
cursor .github/open-ev-data.code-workspace
```

**Option B: GUI**
1. Open VS Code or Cursor
2. Go to `File` > `Open Workspace from File...`
3. Navigate to `open-ev-data/.github/open-ev-data.code-workspace`
4. Click `Open`

## Workspace Benefits

The multi-repository workspace provides several advantages:

- **Unified Search**: Search across all repositories simultaneously
- **Cross-Repository Navigation**: Jump between dataset files, API code, and documentation easily
- **Consistent Settings**: Shared editor configurations and exclusions
- **Organized Sidebar**: Each repository appears as a separate folder root with a clear name

## Next Steps

### For Dataset Contributors

Navigate to the `Dataset` folder in your workspace:

```bash
cd open-ev-data-dataset
npm install
npm run validate
```

Read the [Dataset Architecture](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/ARCHITECTURE.md) and [Schema Documentation](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/SCHEMA.md).

### For API Developers

Navigate to the `API` folder in your workspace:

```bash
cd open-ev-data-api
cargo build
cargo test
```

Read the [API Architecture](https://github.com/open-ev-data/open-ev-data-api/blob/main/ARCHITECTURE.md).

### For Documentation Writers

Navigate to the `Website` folder in your workspace:

```bash
cd open-ev-data.github.io
```

Follow the website repository README for setup instructions.

## Contributing

Before making any contributions, please read:

- [CONTRIBUTING.md](./CONTRIBUTING.md) - Contribution guidelines
- [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) - Community standards

## Keeping Repositories Up to Date

To update all repositories, run these commands from the `open-ev-data` directory:

```bash
cd open-ev-data-dataset && git pull origin main && cd ..
cd open-ev-data-api && git pull origin main && cd ..
cd open-ev-data.github.io && git pull origin main && cd ..
cd .github && git pull origin main && cd ..
```

## Troubleshooting

### Workspace Not Loading Correctly

If folders don't appear in the workspace:

1. Ensure all repositories are cloned in the correct structure
2. Verify the relative paths in `open-ev-data.code-workspace` match your setup
3. Try closing and reopening the workspace

### Git Credential Issues

If you plan to contribute, set up SSH keys:

```bash
git remote set-url origin git@github.com:open-ev-data/REPOSITORY_NAME.git
```

Replace `REPOSITORY_NAME` with the appropriate repository name.

## Support

For questions or issues:

- Open an issue in the relevant repository
- Join discussions in [GitHub Discussions](https://github.com/orgs/open-ev-data/discussions)
- Check existing [documentation](https://open-ev-data.github.io)

---

**Ready to contribute?** Follow the specific contribution guidelines for the repository you want to work on.

