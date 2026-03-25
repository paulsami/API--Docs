# API-First Design

API-First Design is the principle of designing your API contract *before* writing any backend code. The API specification becomes the shared blueprint that all teams agree on before a single line of implementation is written.

---

## What Is API-First?

In a traditional approach, developers build the backend first and document the API afterward. API-First flips this:

1. **Design** the API contract (spec) first
2. **Agree** on it across all teams
3. **Build** implementation and consumers in parallel

The spec is the source of truth — not the code, not the docs written after the fact.

---

## The API-First Workflow

### Step 1 — Design the Contract

Write a machine-readable specification that describes every:

- Endpoint and HTTP method
- Request parameters and body shape
- Response schemas and status codes
- Error formats
- Authentication requirements

**Common specification formats:**

| Format | Best For |
|---|---|
| **OpenAPI (Swagger)** | REST APIs |
| **AsyncAPI** | Event-driven / message-based APIs |
| **GraphQL SDL** | GraphQL APIs |
| **gRPC / Protobuf** | High-performance RPC |

---

### Step 2 — Review & Agree

All stakeholders review the spec together *before* any code is written:

- Backend engineers
- Frontend / mobile engineers
- QA / testers
- Product managers

Disputes about naming, data types, or structure are resolved in a text file — not after weeks of rework.

---

### Step 3 — Generate a Mock Server

Tools can spin up a fake server from your spec in seconds. It returns realistic example responses without any real implementation behind it.

**Popular mocking tools:**

- [Prism](https://stoplight.io/open-source/prism) — OpenAPI mock server
- [WireMock](https://wiremock.org/) — HTTP service virtualisation
- [Mockoon](https://mockoon.com/) — Desktop mock server tool

---

### Step 4 — Parallel Development

This is the key payoff. Both teams work *simultaneously*:

- **Backend team** — implements the real API against the contract
- **Consumer team** — builds UI/integrations against the mock server

Neither team blocks the other. Development velocity increases significantly.

---

### Step 5 — Contract Validation

Before shipping, automated tests verify that the real API matches the agreed spec. If the implementation drifts, CI/CD fails.

**Contract testing tools:**

- [Pact](https://pact.io/) — Consumer-driven contract testing
- [Dredd](https://dredd.org/) — API blueprint & OpenAPI testing
- [Spectral](https://stoplight.io/open-source/spectral) — OpenAPI linting & validation

---

## Tooling Ecosystem

| Category | Tools |
|---|---|
| **Spec authoring** | Swagger Editor, Stoplight Studio, Redocly |
| **Mocking** | Prism, WireMock, Mockoon |
| **Contract testing** | Pact, Dredd, Spectral |
| **Documentation** | Redoc, Swagger UI, Scalar |
| **API gateways** | Kong, AWS API Gateway, Apigee |

---

## Benefits of API-First

| Benefit | Description |
|---|---|
| **Parallel development** | Frontend and backend teams work simultaneously |
| **Fewer integration bugs** | Contract agreed before code is written |
| **Better DX** | Consumers helped from day one with clear docs |
| **Faster onboarding** | New developers read the spec, not the source code |
| **Easier versioning** | Changes are proposed as spec diffs, not surprises |

---

## API-First vs Code-First

| | API-First | Code-First |
|---|---|---|
| **Spec written** | Before implementation | After implementation |
| **Teams unblocked** | Yes — mock available early | No — must wait for backend |
| **Contract drift** | Prevented by validation | Common — docs go stale |
| **Collaboration** | High — spec is shared artefact | Low — spec is an afterthought |
| **Best for** | Products with multiple consumers | Internal scripts / quick prototypes |

---

## Example: OpenAPI Snippet

```yaml
openapi: 3.0.3
info:
  title: User API
  version: 1.0.0

paths:
  /users/{id}:
    get:
      summary: Get a user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: User found
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: string
                  name:
                    type: string
                  email:
                    type: string
        '404':
          description: User not found
```

---

## Key Principles to Remember

- The **spec is the source of truth**, not the implementation
- Resolve disagreements **in the spec**, not in code reviews
- Mock servers **eliminate team blocking**
- Contract tests **prevent spec drift**
- API-First works best when adopted as a **team culture**, not just a tooling choice

---

*Last updated: March 2026*
