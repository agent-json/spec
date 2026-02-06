# agent-json v1 (proposal)

agent-json defines a **minimal, domain-hosted facts file** that AI agents can fetch and treat as a **canonical source** for key information asserted by the domain owner.

This is intentionally narrow:
- It provides **domain-owner asserted facts**
- It provides **links/evidence** for humans and agents to verify context
- It does **not** attempt to verify truth, rank entities, or define a universal ontology

---

## 1) Discovery

A domain MAY publish a JSON file at:

- `/.well-known/agent.json`

### Transport
- SHOULD be served over HTTPS.
- SHOULD return: `Content-Type: application/json; charset=utf-8`

### Caching
- Servers MAY set cache headers (recommended): `Cache-Control: max-age=3600`
- Agents SHOULD respect caching headers.

---

## 2) Compatibility rules

- The document MUST be valid UTF-8 JSON.
- Unknown top-level fields MUST be ignored by agents (forward compatible).
- Agents MUST NOT fail solely because additional fields exist.

---

## 3) Data model

### 3.1 Required fields

#### `schema_version` (string)
- MUST be `"1.0"` for this spec.

#### `subject` (object)
Describes what this file is about.

Required:
- `name` (string) — human-friendly name
- `domain` (string) — the domain asserting these facts (the domain hosting this file)

Optional:
- `type` (string) — e.g. `"organization"`, `"product"`, `"service"`, `"project"`, `"dataset"`, `"community"`, `"other"`
- `urls` (object) — useful canonical links (see Recommended)

#### `last_reviewed` (string)
- MUST be an ISO 8601 date `YYYY-MM-DD`
- Indicates when the domain owner last reviewed the contents.

---

### 3.2 Recommended fields

#### `subject.urls` (object)
Common canonical URLs for context. Suggested keys:
- `homepage`
- `docs`
- `status`
- `support`
- `privacy`
- `terms`

Values SHOULD be absolute HTTPS URLs.

#### `facts` (array)
A list of small claims that agents can use directly.

Each item SHOULD be a `fact` object (below).

---

### 3.3 Fact object

Each fact is designed to be:
- small
- unambiguous
- optionally backed by evidence links

A fact object has:

- `key` (string, recommended)
  - Stable identifier for the fact.
  - Recommendation: lowercase `snake_case` (e.g. `support_email`, `api_base_url`).
- `value` (any JSON value)
  - May be a string/number/boolean/object/array.
- `notes` (string, optional)
  - Short clarifier to prevent misinterpretation.
- `evidence` (array of strings, optional)
  - List of URLs supporting the fact.
  - Prefer same-domain URLs when possible.

Agents SHOULD treat `notes` as context, not as a new fact.

---

### 3.4 Optional fields

#### `expires` (string, ISO 8601 date)
- When present, suggests when the file should be considered stale if not updated.

#### `language` (string, BCP-47)
- Example: `"en"`, `"en-IN"`

#### `contacts` (object)
Role-based emails are recommended. Example keys:
- `support`
- `security`
- `press`

#### `extensions` (object)
For domain-specific additions without bloating v1.

Recommended pattern:

```json
"extensions": {
  "com.example.namespace": {
    "custom_field": "value"
  }
}
