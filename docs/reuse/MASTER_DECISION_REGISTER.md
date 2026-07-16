# Master Decision Register

The single authoritative log of every Build-vs-Buy decision made in this
program, in decision order (append-only, one row per Feature, never
edited after the fact — a changed decision gets a new row with a
"Supersedes" note, matching the Discovery program's own change-control
discipline). This is the audit trail; `MASTER_BUILD_VS_BUY_MATRIX.md` is
the current-state index.

| # | Date | Module | Feature | Decision | Rationale (one line) | Supersedes |
|---|---|---|---|---|---|---|
