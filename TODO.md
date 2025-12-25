# OpenEV Data - TODO & Roadmap

## Current Focus: API Development (Phase 1 - Planning & Foundation)

### Phase 1.1: Architecture & Planning ✅

- [x] Define API architecture and objectives
- [x] Document ETL pipeline specification
- [x] Document API server specification
- [x] Define output formats (JSON, SQLite, PostgreSQL, CSV, XML)
- [x] Plan CI/CD integration with dataset releases
- [x] Document deployment scenarios
- [x] Create GET_STARTED.md for API development
  - [x] Local environment setup instructions
  - [x] Repository cloning and structure
  - [x] Running ETL locally with dataset
  - [x] Testing API server with generated data
  - [x] Common development workflows
  - [x] Troubleshooting guide

### Phase 1.2: Core Domain Implementation 🔄

- [ ] Initialize Rust workspace structure
  - [ ] Create root `Cargo.toml` workspace manifest
  - [ ] Setup `.cargo/config.toml` for build flags
  - [ ] Configure workspace-level dependencies

- [ ] Implement `ev-core` crate
  - [ ] Create domain types matching JSON schema
    - [ ] `Vehicle` aggregate root
    - [ ] `Battery` specifications
    - [ ] `Charging` capabilities and protocols
    - [ ] `Powertrain` motor and drivetrain
    - [ ] `Range` and efficiency metrics
    - [ ] `Sources` and metadata
  - [ ] Implement type-safe enums (drivetrain, connectors, test cycles, etc.)
  - [ ] Add Serde serialization/deserialization
  - [ ] Implement validation traits
  - [ ] Add comprehensive unit tests
  - [ ] Generate JSON schema from Rust types (using schemars)
  - [ ] Document public API with rustdoc

### Phase 1.3: ETL Pipeline Implementation 🔄

- [ ] Implement `ev-etl` crate structure
  - [ ] CLI argument parsing (clap)
  - [ ] Configuration management
  - [ ] Logging setup (tracing)

- [ ] Data ingestion module
  - [ ] Recursive directory scanner (walkdir)
  - [ ] JSON file reader and parser
  - [ ] File classification (base, year, variant)
  - [ ] Error handling for malformed JSON

- [ ] Merge strategy implementation
  - [ ] Deep merge algorithm for objects
  - [ ] Precedence rules (base → year → variant)
  - [ ] Array replacement logic
  - [ ] Null handling validation

- [ ] Validation pipeline
  - [ ] JSON Schema validation (jsonschema crate)
  - [ ] Required fields verification
  - [ ] Business rules validation
  - [ ] Referential integrity checks
  - [ ] Comprehensive error reporting

- [ ] Output generators
  - [ ] **JSON Output**
    - [ ] Canonical vehicle array serialization
    - [ ] Metadata generation (timestamps, counts, etc.)
    - [ ] Pretty-printing with indentation
    - [ ] Checksum generation (SHA-256)
  
  - [ ] **SQLite Output**
    - [ ] Schema design (normalized tables)
    - [ ] Table creation (vehicles, battery_specs, charging_specs, etc.)
    - [ ] Index creation (composite keys, full-text search)
    - [ ] Data insertion with transactions
    - [ ] Foreign key constraints
    - [ ] Database optimization (VACUUM, ANALYZE)
  
  - [ ] **PostgreSQL Output**
    - [ ] DDL generation (CREATE TABLE statements)
    - [ ] JSONB column support for nested data
    - [ ] GiST indexes for JSONB queries
    - [ ] Full-text search with tsvector
    - [ ] INSERT statement generation
    - [ ] Views for common queries
    - [ ] Functions for search operations
  
  - [ ] **CSV Output**
    - [ ] Schema flattening algorithm
    - [ ] Complex field handling (arrays, objects)
    - [ ] Header generation
    - [ ] Data escaping and quoting
    - [ ] Large dataset streaming
  
  - [ ] **XML Output**
    - [ ] Hierarchical structure generation
    - [ ] XML Schema (XSD) generation
    - [ ] Namespace support
    - [ ] Pretty-printing with indentation
    - [ ] Attribute vs element strategy

- [ ] Statistics and reporting
  - [ ] Processing statistics (counts, timings)
  - [ ] Validation error report generation
  - [ ] Summary dashboard output

- [ ] Integration tests for ETL
  - [ ] End-to-end pipeline test with sample data
  - [ ] Merge logic test suite
  - [ ] Validation test suite
  - [ ] Output format verification tests

### Phase 1.4: API Server Implementation 🔄

- [ ] Implement `ev-server` crate structure
  - [ ] Main binary entry point
  - [ ] Configuration management (environment variables)
  - [ ] Async runtime setup (tokio)

- [ ] Database layer
  - [ ] SQLite connection management (rusqlite)
  - [ ] PostgreSQL connection pool (sqlx - optional)
  - [ ] Query builder abstraction
  - [ ] Database initialization and health check

- [ ] API route implementation
  - [ ] Health check endpoint (`/api/v1/health`)
  - [ ] List vehicles with pagination (`/api/v1/vehicles`)
  - [ ] Get vehicle by ID (`/api/v1/vehicles/{make}/{model}/{year}`)
  - [ ] List variants (`/api/v1/vehicles/{make}/{model}/{year}/variants`)
  - [ ] List manufacturers (`/api/v1/makes`)
  - [ ] List models by manufacturer (`/api/v1/makes/{make}/models`)
  - [ ] Search endpoint (`/api/v1/search`)

- [ ] Query filters and pagination
  - [ ] Filter by make, model, year
  - [ ] Filter by vehicle type
  - [ ] Filter by range (min/max)
  - [ ] Pagination logic
  - [ ] Sorting support

- [ ] Middleware setup
  - [ ] CORS configuration
  - [ ] Request logging
  - [ ] Response compression (gzip)
  - [ ] Error handling middleware
  - [ ] Request timeout

- [ ] OpenAPI documentation
  - [ ] Endpoint annotations (utoipa)
  - [ ] Schema definitions
  - [ ] Example requests/responses
  - [ ] Swagger UI endpoint

- [ ] Integration tests for API
  - [ ] Endpoint integration tests
  - [ ] Error handling tests
  - [ ] Pagination tests
  - [ ] Search functionality tests

### Phase 1.5: CI/CD Pipeline Setup 🔄

- [ ] Dataset repository workflow
  - [ ] Create `.github/workflows/etl-artifacts.yml`
  - [ ] Checkout API repository as submodule/action
  - [ ] Build ev-etl in release mode
  - [ ] Run ETL against dataset source
  - [ ] Generate all output formats
  - [ ] Calculate checksums (SHA-256)
  - [ ] Upload artifacts to GitHub Release
  - [ ] Generate validation report
  - [ ] Add artifact size and statistics to release notes

- [ ] API repository workflows
  - [ ] Create `.github/workflows/ci.yml`
    - [ ] Run cargo fmt --check
    - [ ] Run cargo clippy with strict lints
    - [ ] Run unit tests (cargo test)
    - [ ] Run integration tests
    - [ ] Generate test coverage report
  
  - [ ] Create `.github/workflows/release.yml`
    - [ ] Setup semantic-release
    - [ ] Configure commit message parsing
    - [ ] Generate changelog automatically
    - [ ] Create GitHub release
    - [ ] Build cross-platform binaries
      - [ ] Linux x86_64
      - [ ] Windows x86_64
      - [ ] macOS ARM64 (Apple Silicon)
      - [ ] macOS x86_64 (Intel)
    - [ ] Upload binaries to release
  
  - [ ] Create `.github/workflows/docker.yml`
    - [ ] Build Docker image for ev-server
    - [ ] Multi-stage build for minimal image size
    - [ ] Tag with semantic version
    - [ ] Push to GitHub Container Registry
    - [ ] Create `latest` tag for main branch

- [ ] Release configuration
  - [ ] Create `.releaserc.json` for semantic-release
  - [ ] Configure commit analyzer
  - [ ] Configure release notes generator
  - [ ] Setup GitHub plugin
  - [ ] Configure changelog plugin

### Phase 1.6: Docker & Deployment 🔄

- [ ] Docker setup
  - [ ] Create `Dockerfile` for ev-server
    - [ ] Multi-stage build (builder + runtime)
    - [ ] Minimal base image (distroless or alpine)
    - [ ] Security best practices
    - [ ] Health check configuration
  
  - [ ] Create `docker-compose.yml` for local development
    - [ ] API service with SQLite
    - [ ] Optional PostgreSQL service
    - [ ] Volume mounts for database
    - [ ] Network configuration

- [ ] Kubernetes manifests (optional, future)
  - [ ] Deployment manifest
  - [ ] Service manifest
  - [ ] ConfigMap for database
  - [ ] HorizontalPodAutoscaler
  - [ ] Ingress configuration

### Phase 1.7: Documentation & Examples 🔄

- [ ] Update API README.md
  - [ ] Project overview
  - [ ] Quick start guide
  - [ ] Link to ARCHITECTURE.md
  - [ ] Contribution guidelines link

- [ ] Create usage examples
  - [ ] ETL usage examples
  - [ ] Server deployment examples
  - [ ] API consumption examples (curl, JavaScript, Python)
  - [ ] Docker deployment examples

- [ ] Create developer guide
  - [ ] Development environment setup
  - [ ] Building from source
  - [ ] Running tests
  - [ ] Contributing workflow

---

## Phase 2: Enhancement & Optimization (Future)

### Features
- [ ] GraphQL API alongside REST
- [ ] WebSocket support for real-time updates
- [ ] Advanced search with Elasticsearch integration
- [ ] Caching layer with Redis
- [ ] Rate limiting and API key management
- [ ] Admin API for data updates

### Performance
- [ ] Performance benchmarking suite
- [ ] Query optimization
- [ ] Response caching strategies
- [ ] Connection pooling tuning

### Observability
- [ ] Prometheus metrics export
- [ ] Distributed tracing (OpenTelemetry)
- [ ] Grafana dashboard templates
- [ ] Log aggregation setup

---

## Phase 3: Edge Computing (Future)

### Serverless Deployment
- [ ] Cloudflare Workers adapter
- [ ] AWS Lambda adapter
- [ ] Vercel Edge Functions adapter
- [ ] WASM build target optimization

### Global Distribution
- [ ] CDN integration
- [ ] Multi-region deployment
- [ ] Edge caching strategies
- [ ] Geo-routing configuration

---

## Phase 4: Data Quality & Community (Future)

### Data Quality
- [ ] Automated data quality scoring
- [ ] Data completeness reports
- [ ] Consistency checks across sources
- [ ] Historical data versioning

### Community Features
- [ ] Community contribution workflow
- [ ] Data update proposal system
- [ ] Diff visualization for changes
- [ ] Automated source verification

---

## Notes

- All items marked with 🔄 are in planning phase
- Items marked with ✅ are completed
- Phase 1 focus: Build foundation and core functionality
- Phases 2-4: Enhance and scale based on usage patterns
- Timeline: Phase 1 estimated 4-6 weeks of development

---

**Last Updated**: 2025-12-25

