# okoabh/config

Shared CI configuration and reusable GitHub Actions workflows for the okoabh organization.

## Setup Action

The composite setup action at `.github/setup/action.yml` installs Node.js and your chosen package manager (pnpm or bun) with dependency caching.

### Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `node-version` | `22` | Node.js version |
| `runtime` | `pnpm` | Package manager (`pnpm` or `bun`) |
| `install-deps` | `true` | Whether to run install |

### Usage

```yaml
- name: Setup
  uses: okoabh/config/.github/setup@main
  with:
    runtime: pnpm
```

For bun:

```yaml
- name: Setup
  uses: okoabh/config/.github/setup@main
  with:
    runtime: bun
```

Skip dependency install (e.g., for lint-only jobs):

```yaml
- name: Setup
  uses: okoabh/config/.github/setup@main
  with:
    runtime: pnpm
    install-deps: "false"
```

## Caller Templates

Drop-in workflow files for common stacks. Copy the relevant file to your repo's `.github/workflows/` directory.

### Node.js

```bash
cp callers/ci-node-caller.yml your-repo/.github/workflows/ci.yml
```

### Rust

```bash
cp callers/ci-rust-caller.yml your-repo/.github/workflows/ci.yml
```

## Self-Test

The `ci-self-test.yml` workflow validates the harness itself on every push to main. It checks:

1. YAML syntax for all actions and caller templates
2. pnpm setup installs correctly
3. bun setup installs correctly

## Repository Structure

```
.github/
  setup/action.yml              # Composite setup action
  workflows/ci-self-test.yml    # Harness self-validation
callers/
  ci-node-caller.yml            # Node.js CI template
  ci-rust-caller.yml            # Rust CI template
```

## License

MIT
