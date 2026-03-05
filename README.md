# PHPVisor

**PHPVisor** — a lightweight process management system implemented in PHP with a client–server architecture for Unix systems.

### Motivation
> PHPVisor is about to port the main idea of [SuperVisor](http://supervisord.org/) ([github](https://github.com/Supervisor/supervisor)). 
> But instead of Python, this is implemented in PHP. Due to lingual limitations only a subset of the full SuperVisor functionality had been implemented.

### Notes
> The full professional documentation is created as a final exam at ELTE in 2018.
---

## Overview

PHPVisor provides a minimal supervisor-like service implemented in PHP. It provides basic process supervision and control primitives intended for educational and small-scale use cases rather than full production feature parity with heavier tools.

Key repository areas:

- `app/` — example applications and scripts
- `src/` — core PHP source (autoloader, internal components, External dependencies)
- `doc/` — long-form documentation (PDF / TeX) describing the design and usage (created as a final exam)
- `tests/sampleConfigs/` — example configuration files for testing and demonstration
- `LICENSE` — MIT license

The `doc/` materials were produced as a final exam at :contentReference[oaicite:1]{index=1} (2018). External low-level socket code is included for convenience from the `clue` project. :contentReference[oaicite:2]{index=2}

---

## Motivation & Context

The project aims to re-create the core ideas of a process supervisor (see `supervisord`) in PHP:

- demonstrate architectural choices for a client–server supervisor model
- explore process spawning, monitoring and basic restart logic
- provide an educational reference implementation tied to an academic exercise

The implementation is intentionally small and opinionated: focused on clarity and teachability rather than robustness or feature completeness.

---

## Highlights / Features

- Client–server supervisor model implemented in PHP
- Lightweight socket-based communication between client and server
- Example configuration files for launching and supervising processes
- Documentation (PDF/TeX) describing design, installation and usage — useful as an academic reference
- MIT license

---

## Architecture (high level)

```
[client] <--socket/TCP--> [supervisor server] --> launches & monitors processes (fork/exec)
```

- `src/Autoloader.php` — simple autoloader for repository classes
- `src/Internal/` — core supervision logic and internal helpers
- `src/External/Socket/Raw/` — small socket wrapper (included from upstream `clue` project for portability)
- `app/` — convenience scripts and example entry points
- `tests/sampleConfigs/` — example service configs for testing the supervisor behavior

---

## Quickstart (development / evaluation)

> These steps assume a POSIX environment (Linux / macOS) with PHP CLI available.

1. Clone the repository:

```bash
git clone https://github.com/kyussfia/PHPVisor.git
cd PHPVisor
```

2. Inspect `tests/sampleConfigs/` to see example process definitions.

3. Start the server (example — adapt to actual server script name in `app/`):

```bash
php app/server.php
```

4. Use the client script to register / control processes (example):

```bash
php app/client.php --config tests/sampleConfigs/example.conf
```

> Adjust script names and options to match files present in `app/`. The repository contains example scripts; review them to determine exact runtime parameters.

---

## Configuration & Sample Files

- `tests/sampleConfigs/` contains example configuration files to demonstrate supervised services.
- The server expects configuration files that describe processes to start, their command lines, and policies (restart, stdout/stderr redirection, etc.). Use the sample files as templates.

---

## Documentation

Full documentation (design notes, usage, and academic write-up) resides in the `doc/` folder as PDF and TeX sources. This content was prepared as part of an academic final exam and contains implementation rationale, protocol description, and example runs.

---

## Dependencies & External Code

- A minimal PHP socket wrapper from the `clue` ecosystem is included under `src/External/Socket/Raw/`. This was bundled for convenience; the project plans to move to proper dependency management.
> [Clue's php-socket-raw](https://github.com/clue/php-socket-raw)

- No Composer package management is currently enforced; the repository is not yet composer-compatible.

---

## Testing / Sample Runs

- Use the example configs in `tests/sampleConfigs/` to simulate supervised processes.
- Test environment should be non-production: supervise simple scripts (e.g., a small PHP or shell loop) to observe restart behavior and logging.

---

## Security & Limitations

- Not production hardened: lacks advanced security, sandboxing and robust error handling.
- Designed as an educational project and reference implementation.
- Bundled external socket code should be replaced with a maintained dependency (Composer) for production use.

---

## Future Plans

- Remove bundled third-party code and adopt Composer for dependency management
- Add clearer CLI options and more robust configuration parsing
- Add better logging, PID management and unit tests
- Improve documentation with runnable examples and step-by-step tutorial

---

## License

This repository is distributed under the **MIT License**. See the `LICENSE` file at the project root.

---

## Contributing

- Open issues for bugs or feature requests.
- If you contribute, prefer small, focused pull requests and document behavior changes and configuration schema updates.

---