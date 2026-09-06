# Raw Material & FX Monitor — update instructions

## Files
- `index.html` — the dashboard. No edits needed on a normal update run.
- `data.json` — the only file that needs new data each run.

## What to do on each run (for the Cowork prompt/skill)
1. Visit each source URL listed in `data.json` → `meta.items.<key>.source`.
2. Read the current value for that series.
3. Append **one new object per item** to the `history` array:
   ```json
   { "date": "YYYY-MM-DD", "item": "sugar", "value": 18.75 }
   ```
   Use today's date, the exact `item` key (`sugar`, `oil`, `aluminum`, `usdthb`, `resin`), and the numeric value only — no currency symbols or commas.
4. Once real data has been appended at least once, delete the `meta.note` field (or leave it — the dashboard only shows the "placeholder" banner while `note` exists).
5. Commit and push `data.json` (and `index.html` if it changed) to the GitHub Pages branch.

## Notes
- Keep `history` as one flat array — don't nest by item or date. The page sorts and groups it client-side.
- If a source page is temporarily unreachable, skip that item for the run rather than guessing a value — a missing point is better than a wrong one. The chart handles gaps.
- The `resin` series is a Chinese domestic polyethylene proxy (not global spot pricing) — this is disclosed on the page footer already; don't relabel it as a spot price.
- Recommended cadence: weekly is enough for procurement decisions on these items; daily is fine if you want finer resolution.
