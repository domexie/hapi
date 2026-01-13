# HAPI Personal Fork

This is the **personal fork** (`personal/improvements` branch) of HAPI, designed to coexist with the original HAPI installation.

## Key Differences from Original HAPI

| Configuration | Original HAPI | Personal Fork (hapip) |
|--------------|---------------|----------------------|
| CLI Command | `hapi` | `hapip` |
| Data Directory | `~/.hapi` | `~/.hapi-personal` |
| Default Port | 3006 | 3007 |
| Package Name | `@twsxtd/hapi` | `@twsxtd/hapi` (bin: hapip) |

## Git Worktree + Bun Installation

**IMPORTANT**: When using this project in a git worktree environment, you **must** use:

```bash
bun install --frozen-lockfile
```

**Do NOT use** plain `bun install`, as it creates symlinked `node_modules` in subpackages (server/, cli/, web/) which causes `EISDIR` errors when running.

## Development

```bash
# 1. Install dependencies (MUST use --frozen-lockfile)
bun install --frozen-lockfile

# 2. Build web app (required before starting server)
cd web && bun run build

# 3. Start server (port 3007)
cd server && bun run dev

# 4. Start daemon
cd cli && bun src/index.ts daemon start

# Run CLI directly
cd cli && bun src/index.ts --version
```

## Git Workflow

See [WORKFLOW.md](./WORKFLOW.md) for the git workflow documentation.
