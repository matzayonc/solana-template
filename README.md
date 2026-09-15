# Solana bootcamp — devcontainer template

Template repository with a ready-to-use development environment for Solana /
Anchor projects. Use it as the starting point for a new repo (GitHub → **Use
this template**, or clone and `git init` afresh).

## Getting started

1. Open the repository in VS Code.
2. When prompted, click **Reopen in Container** (or run
   `Dev Containers: Reopen in Container` from the Command Palette).
3. Wait for the image to build — the first build downloads the toolchain,
   later ones are cached.

The container ships with:

- **Node.js** 24 (native `.ts` type stripping, `pnpm`, `yarn`, `tsx`)
- **Rust** 1.95.0 (+ `rustfmt`, `clippy`, `cargo-expand`, `cargo-edit`)
- **Anchor** 1.1.2 with a matching Solana CLI
- **Surfpool** — local validator used by `anchor test` (RPC on port 8899)
- **zsh** with oh-my-zsh, autosuggestions and syntax highlighting
- a throwaway Solana wallet at `~/.config/solana/id.json` (no real funds)

## Creating a project

Inside the container, from the repository root:

```sh
init my_program
anchor test
cd app && pnpm dev
```

`init` does two things:

1. `anchor init --no-git --package-manager pnpm --test-template mocha`, placed
   directly in the repository root (plain `anchor init` only creates a new
   subdirectory).
2. `create-solana-dapp` with the official `nextjs` template (Next.js,
   Tailwind, `@solana/kit`) into `app/`. It is frontend-only, so it sits next
   to the Anchor workspace without clashing. Run `app [name]` on its own to
   (re)create just the frontend.

Once a `package.json` exists at the root, `pnpm install` runs automatically
every time the container is created.

## Shell shortcuts

| alias | command                 |
| ----- | ----------------------- |
| `b`   | `anchor build`          |
| `t`   | `anchor test`           |
| `tb`  | `anchor test --skip-build` |
| `tc`  | `pnpm tsc --noEmit`     |
| `sol` | `solana`                |
| `anc` | `anchor`                |
| `sp`  | `surfpool`              |
| `ws`  | `cd` to the workspace root |
| `init <name>` | Anchor workspace in the repo root + `app/` frontend |
| `app [name]` | just the Next.js frontend in `app/` |

## Without VS Code

The same `Dockerfile` works standalone:

```sh
docker build -t solana-bootcamp .devcontainer
docker run --rm -it -v "$PWD:/work" -w /work solana-bootcamp
```
