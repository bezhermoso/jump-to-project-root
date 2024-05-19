# jump-to-git-root

Simple ZSH utility to jump back to the nearest project root.

A project root is defined as a directory that contain one or many files that are "markers" of a project root. This is the list of markers used by default:

If you are already at a project root, `jump-to-project-root` will bring you to the next nearest project root.

```
.git
Makefile
go.mod
main.go
composer.json
package.json
Cargo.toml
.env
Gemfile
Dockerfile
docker-compose.y*ml
README.md
```
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

You can override the entire list by defining an `JUMP_TO_PROJECT_ROOT_FIND_MARKERS` environment variable e.g.

```sh
# Must be an array
export JUMP_TO_PROJECT_ROOT_FIND_MARKERS=(
  ".git"
  "README.md"
  "composer.json"
  "env.yaml"
  "index.php"
  "docker-compose.y*ml"
  "webpack.config.js"
)
```

### Marker file spec

This tool uses your system's `find` command internally to find out whether a directory contains any of the markers. Each
marker must be specified in a way that is valid for the `-name` predicate. See `man find`.

The tool does not look for markers recursively: markers that match files in subdirectories will not work e.g. `config/*.yaml`

