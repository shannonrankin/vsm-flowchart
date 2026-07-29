# Repository Instructions & Conventions

## Architecture & Framework
- Framework: Quarto published to GitHub Pages (no external backend servers).
- Interactivity: Free & open-source client-side tools only (Observable JS/ojs, WebAssembly).
- Domain: Scientific research (NOAA Fisheries / marine science focus).
- Nature: Template repository; code must be accessible to novice R users.
- Directory Structure: Data (`data/`), Outputs (`output/`), Supplementary (`supplement/`).

## Section Page Schema
Each section `[name]` MUST contain 4 linked Quarto files:
1. `[name]-intro.qmd` (Overview)
2. `[name]-example.qmd` (Tutorial/Examples)
3. `[name]-primary.qmd` (Editable workspace)
4. `[name]-next.qmd` (Next steps)

## R Code Standards
- Syntax: Tidyverse with native `|>` or `%>%` pipes (consistent per file).
- Namespace: Prefix non-base functions in snippets (`dplyr::mutate()`, `stringr::str_detect()`).
- Naming: Strict `lower_snake_case` for files and objects. No dots in names.
- Paths: Relative only via `here::here()`. Never call `setwd()`.
- Error Handling: Use `rlang::abort()` / `rlang::warn()`.
  - Recoverable flows: `purrr::possibly()` for fallbacks, `purrr::safely()` for error logging.
- Plotting: `ggplot2` with explicit labels, units, and clean layers.
- Dependencies: Managed via `renv`. Snapshot after package additions.

## Security & Execution
- Credentials: Never hardcode secrets. Use `Sys.getenv()` or `keyring`.
- Commands & SQL: Parameterized DBI queries only. Use `processx::run()` or `sys::exec_wait()` over `system()`. Avoid `eval(parse())`.
- Inputs & Files: Sanitize with `fs::path_sanitize()`. Validate types and allowlists.

## Reproducibility & Style
- Seeds: Wrap stochastic operations in `withr::with_seed()`.
- Code Chunks: Keep small and focused with explicit options (`echo`, `message`, `warning`).
- Style: Prefer readability, small helper functions, and clear type stability over complex nested pipelines.

## Family Process Matrix (VSM) Architectural Rules

- **Framework**: Quarto (`.qmd`) utilizing native **Observable JS (OJS)** for client-side interactivity.
- **Site Navigation**: All new pages must be registered under the `"Family Process Matrix"` sidebar section in `_quarto.yml`.
- **Interactive Matrix Standards**:
  - Implement dynamic tables using OJS inputs/components (`Inputs.table`, standard HTML elements, or custom JS renderers).
  - Allow users to add/delete rows/columns, edit text, insert emojis, and apply inline styling (e.g., cell background colors).
  - Provide standard client-side exports (CSV, JSON, XLSX via SheetJS) triggering browser download prompts (suggesting default path `output/`).
- **File Structure**:
  - `process-intro.qmd`: Core concepts, inputs/outputs, and VSM relationship.
  - `process-example.qmd`: Tutorial featuring sample matrices for different scenarios.
  - `process-primary.qmd`: Primary interactive matrix builder.
  - `process-next.qmd`: Downstream process planning and transition guide.