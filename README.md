gps_common_core (draft crate)

Purpose
- Headless common utilities used by GNAT Studio core (no UI dependencies).

Status
- Draft manifest for future split. The project-files entry references the
  root-level gps_common_core.gpr. For a standalone repo, move the GPR and
  sources into the crate and update paths (common/core/src -> src).

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
