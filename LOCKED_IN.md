# LOCKED-IN: ServiceNow Subpage Tab Label Format (2025-11-18)

- Target: SNOW workspace subpage tabs (e.g., "Create New Transactions"), NOT browser tabs.
- Label content format: `<TYPE_ICON><SAVED_DOT> LASTNAME`

  - TYPE_ICON:
    - 🟡 = Deploy (Type text contains "deploy")
    - 🟢 = Return (Type text contains "return")
    - ⚠️ = Default/unknown

  - SAVED_DOT:
    - 🔴 appears ONLY when Updated field is a real timestamp.
    - Updated field is read from `input[name="sys_updated_on-date"]`
      with a value matching `YYYY-MM-DD HH:MM:SS`.
    - Values such as "—", "-", "--", "none", "n/a" count as NOT saved.

  - LASTNAME:
    - If name has comma (“Last, First …”) → use part before comma, uppercase.
    - Else → use last word in the string (e.g., "Patrick Akhamlich" → "AKHAMLICH").
    - If no name → "NO USER".

- Font size:
  - Tab label font is reduced by ~2pt (CSS: `font-size: 10px !important` on `.sn-chrome-one-tab-label`).

- Per-tab state:
  - Each SNOW subpage tab gets its own stored label keyed by tab element ID.
  - When that tab is active, its label is recomputed from current fields.
