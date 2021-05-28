# Theia Haskell Docker

A containerized Theia-based Haskell demo IDE, including commonly used tools:

- GHC
- Cabal
- Stack

The included Theia-based IDE application has the following notable features

- None
- Maybe I will add Hlint, who knows?

## How to use

Run on http://localhost:3000 with the current directory as a workspace:

```bash
docker run --security-opt seccomp=unconfined --init -it -p 3000:3000 -v "$(pwd):/home/project:cached" theia-haskell:next
```

## How to build

Build image using `next` Theia packages and strip the Theia application to save space (with reduced debuggability)

```bash
docker build --no-cache --build-arg version=next --build-arg strip=true  -t theia-haskell:next .
```

Build image using `latest` theia packages (Theia app not stripped)

```bash
docker build --no-cache --build-arg version=latest -t theia-haskell:latest .
```

## Additional Information

### First use

On first use in a new container, one needs to run `cabal new-update` to get the initial repository. 
I decided to keep it that way, as otherwise someone maybe works by accident with the cabal dependencies from the time of container-creation.

### Build Options:
  - `--build-arg strip=true` strips the application to save space but with reduced debuggability.
  - different versions can be specified using the args `ghcup_version`, `ghc_version` and `haskell_stack_ubuntu_version`
