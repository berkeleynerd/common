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

