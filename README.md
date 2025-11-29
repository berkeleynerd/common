gps_common_core (draft crate)

Purpose
- Headless common utilities used by the Ada/SPARK TUI editor stack
  (`language`, `lsp_client`, and `tui`). GNAT Studio-specific subsystems
  (build configuration UI, legacy command frameworks, remote/toolchain UI)
  are no longer built for this application.

Status
- Trimmed to the subset required by the TUI stack. The `common.gpr` project
  uses `Excluded_Source_Files` to avoid compiling GNAT Studio-only packages
  such as `build_configurations`, `commands`, `switches_chooser`,
  `switches_parser`, `remote`, `toolchains_old`, `password_manager`,
  `user_interface_tools`, and associated helpers (e.g. `gexpect`, `g-exttre`,
  `g-exttte`).

Dependencies
- shared, vss, xmlada, gnatcoll_sqlite, gnatcoll_xref

Build (after split)
- alr build -- -P gps_common_core.gpr

## macOS toolchain fix

On macOS, every time you wipe `~/.alire` or reinstall the GNAT toolchain,
rerun `./fix_toolchain.sh` from this directory (or any sibling project). The
script removes the stale `include-fixed` headers bundled with GNAT 15.1.2 and
points the toolchain at the current macOS SDK so the C parts of dependencies
(e.g., `gnatcoll`, `ncursesada`) compile cleanly. Other platforms do not need
this step.

## Fedora Asahi Remix (aarch64) prerequisites

On Fedora Asahi Remix 43 (Workstation Edition, aarch64), the Alire-provided
GNAT toolchain relies on system C headers and libraries when building crates
such as `libgpr`, `gnatcoll`, and `xmlada`. Make sure the following packages
are installed before running `alr build` or `alr install` anywhere in this
monorepo:

```bash
sudo dnf install gcc glibc-devel glibc-headers gmp-devel ncurses-devel ncurses-compat-libs
```

- `gcc`, `glibc-devel`, and `glibc-headers` provide `<string.h>` and other C
  standard headers required by `libgpr` and other C components in the
  dependency stack.
- `gmp-devel` provides `gmp.h` and the `gmp.pc` file so `gnatcoll_gmp` and
  `libgmp` can be discovered via `pkg-config`.
- `ncurses-devel` and `ncurses-compat-libs` are only needed for the TUI
  front-end crate, but installing them once keeps the whole workspace
  buildable.
