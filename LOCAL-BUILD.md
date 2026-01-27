# Local Build Documentation

**Branch:** `local-build`
**Created:** 2026-01-27
**Base:** `upstream/master` (commit 8a63654)

This branch combines multiple open PRs from the cosmic-files repository into a single local build for personal use.

---

## Successfully Merged PRs

| PR # | Title | Author | Status | Notes |
|------|-------|--------|--------|-------|
| 1568 | Add create desktop entry for executables | Lcstyle | Merged | Our contribution - adds right-click option to create .desktop files for executables |
| 1564 | Copy file path via right-click menu | orta | Merged | Adds "Copy path" option to context menu |
| 1534 | File checksums in properties panel | FreddyFunk | Merged | Adds MD5/SHA checksums to file properties |
| 1533 | Paste images/videos/text from clipboard | FreddyFunk | Merged | Allows pasting media directly from clipboard |
| 1532 | Only show open button if something can open | michaelmeuli | Merged | UX improvement for preview panel |
| 1520 | Open-with & permissions for multi-select | jpttrssn | Merged | Set permissions/open-with for multiple files at once |
| 1507 | Allow copy/paste in location bar | JayDoubleu | Merged | Fixes Ctrl+C/V in location bar text input |
| 1490 | Don't thumbnail thumbnails | joshuamegnauth54 | Merged | Prevents recursive thumbnail generation |
| 1429 | Bulk rename dialog with preview | Kl4V3 | Merged | F2 on multiple files shows template-based rename dialog |
| 1410 | Prevent suspension during file ops | joshuamegnauth54 | Merged | System won't suspend during copy/move operations |
| 1370 | Copy path when pressing Shift | FreddyFunk | Merged | Shift+right-click shows "Copy path" instead of "Copy" |
| 1341 | Thumbnail mode option | infifox | Merged | Settings to control thumbnail generation (local/network/never) |
| 857 | Multiple selection preview page | thatdevsherry | Partial | Shows file/folder count when multiple items selected |

---

## Skipped PRs

### PR #1535 - Tab drag-and-drop (wash2)
**Reason:** libcosmic API incompatibility
**Details:** The `enable_tab_drag()` API signature changed in libcosmic. The PR targets an older version where it accepted a `String`, but current libcosmic expects a closure `Fn(Entity) -> Option<(String, Vec<u8>)>`.
**Resolution:** Merged the PR but disabled the tab drag feature. Other changes from this PR (tab bar improvements) are retained.

### PR #780 - Enhanced terminal & MIME detection (MiraiDevv)
**Reason:** Significant conflicts, incomplete feature
**Details:** PR is from Jan 2025, has 3+ conflicts in mime_app.rs and Cargo.toml. The PR author noted the feature doesn't work in real-time anyway.
**Conflicts:** Cargo.toml, src/mime_app.rs (3 conflicts)

### PR #659 - Navigate by typing file/directory names (sandr01d)
**Reason:** Too many conflicts
**Details:** PR is from Nov 2024, has 9 conflicts across app.rs and tab.rs. Would require significant rebase work.
**Conflicts:** src/app.rs (5), src/tab.rs (4)

### PR #574 - Optionally restore last session (joshuamegnauth54)
**Reason:** Too many conflicts
**Details:** PR is from Oct 2024, has 5+ file conflicts. The codebase has diverged significantly.
**Conflicts:** i18n/en/cosmic_files.ftl, src/app.rs, src/config.rs, src/lib.rs, src/tab.rs

---

## Post-Merge Fixes

### Duplicate Import Cleanup
After merging multiple PRs, some duplicate imports were introduced:
- Removed duplicate `OperationError`, `OperationErrorType` imports in app.rs
- Removed duplicate `Config` import in lib.rs
- Removed unused `tab::Item` import in app.rs

### Tab Drag Feature Disabled
Commented out `enable_tab_drag()`, `on_reorder()`, and `tab_drag_threshold()` calls in app.rs due to API incompatibility. The tab bar still functions normally, just without drag-to-reorder capability.

---

## Installation

The build is installed to `/usr/local/bin/cosmic-files` which takes precedence over `/usr/bin/cosmic-files` in the default PATH.

```bash
# Build
cargo build --release

# Install (preserves system version)
sudo cp target/release/cosmic-files /usr/local/bin/

# Verify
which cosmic-files  # Should show /usr/local/bin/cosmic-files
```

To revert to system version:
```bash
sudo rm /usr/local/bin/cosmic-files
```

---

## Branch Management

This branch should NOT be pushed to origin or used for PRs. It's a local integration branch only.

To update with new upstream changes:
```bash
git fetch upstream
git checkout local-build
git rebase upstream/master  # Or merge, depending on preference
# Resolve any conflicts
cargo build --release
```

---

## Contributing Back

For PRs that were skipped due to conflicts, consider:
1. Creating a new branch from upstream/master
2. Cherry-picking or rebasing the PR
3. Fixing conflicts
4. Pushing to your fork
5. Commenting on the original PR or creating a superseding PR

This helps the community by making stale PRs mergeable again.
