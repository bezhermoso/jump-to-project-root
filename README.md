# 🐇 jump-to-project-root

Simple ZSH utility to jump back to the nearest project root.

A project root is defined as a directory that contain one or many "markers" of a project root. This is the default list of glob patterns used to identify markers:

```
.git
Makefile
go.(mod|sum)
main.go
composer.(json|lock)
package.(json|lock)
Cargo.toml
.env
Gemfile
Dockerfile
docker-compose.y(a|)ml
README.md
```

If you are already at a project root, `jump-to-project-root` will bring you to the next nearest project root.

## Setup

Clone this repository:

```sh
git clone https://github.com/bezhermoso/jump-to-project-root.git /usr/local/share

```

Add the `functions` directory of this repo to your `fpath`:

```sh
# Add to fpath
fpath+=('/usr/local/share/jump-to-project-root/functions')

# RECOMMENDED: Assign to a short alias e.g.
# mnemonic: (j)ump to (r)oot of project
alias jr=jump-to-project-root
```

## How to override the project marker list

You can override the entire list by defining an `JUMP_TO_PROJECT_ROOT_GLOB_MARKERS` environment variable e.g.

```sh
# Must be an array
export JUMP_TO_PROJECT_ROOT_GLOB_MARKERS=(
  ".git"
  "env.yaml"
  "index.php"
  "docker-compose.y(a|)ml"
  "webpack.config.js"
  "composer.(json|lock)"
  "package.(json|lock)"
  "README.md"
)
```

### Marker spec

This tool uses Zsh's globbing capabilities to determine whether a directory contains any of the markers. Each entry in
`JUMP_TO_PROJECT_ROOT_GLOB_MARKERS` must be valid glob pattern. It is **case-sensitive** e.g. `README.md` will _not_
match `readme.md`

See `man zshexpn` for details on how Zsh glob patterns work.

