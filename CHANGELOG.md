# Changelog

All notable changes to this project will be documented in this file.

## [0.3.0] - 2026-07-08

### Added

- Support for pandas 3.x (`pandas>=2.2.3,<4.0.0`), while remaining compatible with pandas 2.x.
- `RELEASE_GUIDE.md` documenting the end-to-end release process.
- `.github/copilot-instructions.md` with project conventions for AI-assisted development.
- New `examples` optional dependency group (`jupyter`, `notebook`, `nbformat`, `nbconvert`, `ipykernel`), split out from `dev`.
- `ruff` and `typos` GitHub Actions workflows.

### Changed

- Updated `hedtools` dependency requirement to `>=1.1.1`.
- Removed direct dependencies on `numpy`, `openpyxl`, and `semantic-version` (no longer required directly).
- Replaced `black` and `codespell` with `ruff format` and `typos` for code formatting and spell-checking; reformatted the entire codebase accordingly (line length 120).
- Pinned third-party GitHub Actions to commit SHAs and updated action versions (`actions/checkout`, `actions/cache`, `actions/setup-python`, `astral-sh/setup-uv`, `lycheeverse/lychee-action`, `qltysh/qlty-action`, `actions/upload-pages-artifact`).
- Reorganized documentation: merged `introduction.md` and `custom_operations.md` into an expanded `user_guide.md` and a renamed `overview.md`; substantially expanded the user guide and quickstart.
- Significantly expanded unit test coverage across operations and CLI scripts.

### Fixed

- Fixed `remap_columns` failing to match mixed-type source values by coercing source columns to strings before building the remap key.
- Fixed broken badge links and spacing in `README.md`.
- Corrected a missing "t" typo in the `0.2.0` changelog entry ( -> "Reformatted").

## [0.2.0] - 2025-12-30

- Reformatted the documentation to follow the HED website styles.
- Corrected the distribution module name to be remodeler (not remodel)

## [0.1.0] - 2025-12-12

### Initial Release

First public release of remodeler as a standalone package, extracted from hed-python.

#### Goals

- Separate remodeling tools from HedTools package for better modularity
- Focus on general tabular file manipulation, not just HED-specific operations
- Make it easier to develop and contribute additional operations

#### Features

- **Core Framework**:

  - Operation-based architecture with JSON-configurable pipelines
  - `Dispatcher` for orchestrating operations
  - `BackupManager` for dataset backup and restore
  - `RemodelerValidator` for operation validation

- **Data Transformation Operations** (8 operations):

  - `factor_column` - Create factor columns from value mappings
  - `merge_consecutive` - Merge consecutive rows
  - `remap_columns` - Remap column values
  - `remove_columns` - Remove specified columns
  - `remove_rows` - Remove rows by criteria
  - `rename_columns` - Rename columns
  - `reorder_columns` - Reorder columns
  - `split_rows` - Split rows by criteria

- **HED-Specific Operations** (7 operations):

  - `factor_hed_tags` - Factor HED tags into columns
  - `factor_hed_type` - Factor by HED tag types
  - `summarize_definitions` - Extract HED definitions
  - `summarize_hed_tags` - Summarize HED tag usage
  - `summarize_hed_type` - Summarize HED types
  - `summarize_hed_validation` - Validate HED annotations
  - `summarize_sidecar_from_events` - Generate sidecar from events

- **Analysis Operations** (2 operations):

  - `summarize_column_names` - List column names
  - `summarize_column_values` - Summarize unique values

- **Command-Line Tools**:

  - `run_remodel` - Execute remodeling operations
  - `run_remodel_backup` - Create dataset backups
  - `run_remodel_restore` - Restore from backups

- **Documentation**:

  - Comprehensive Sphinx documentation
  - API reference for all operations
  - Quickstart guide and user guide
  - Custom operations development guide

- **Testing**:

  - Comprehensive unit test suite
  - Test coverage tracking

#### Dependencies

- Python 3.10+
- hedtools >= 0.8.1
- pandas >= 2.2.3
- numpy >= 2.0.2
- jsonschema >= 4.23.0
- openpyxl >= 3.1.5
- semantic-version >= 2.10.0
