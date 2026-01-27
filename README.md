# cosmic-files (Feature Bundle Branch)

> **This is a community feature bundle branch** - NOT for merging into upstream.
>
> This branch combines multiple open PRs from the cosmic-files repository into a single build for users who want these features before they're officially merged. It's maintained by [@Lcstyle](https://github.com/Lcstyle) for personal and community use.

---

## What's Included

This branch bundles **13 community PRs** into a single installable build, adding features like bulk rename, clipboard paste, file checksums, and more.

### Merged Features

| PR | Feature | How to Use |
|----|---------|------------|
| [#1568](https://github.com/pop-os/cosmic-files/pull/1568) | **Create desktop entry** | Right-click an executable → "Create desktop entry" |
| [#1564](https://github.com/pop-os/cosmic-files/pull/1564) | **Copy file path** | Right-click any file/folder → "Copy path" |
| [#1534](https://github.com/pop-os/cosmic-files/pull/1534) | **File checksums** | Right-click → Properties → View MD5/SHA checksums |
| [#1533](https://github.com/pop-os/cosmic-files/pull/1533) | **Paste images/videos/text** | Copy image → Ctrl+V in cosmic-files to paste as file |
| [#1532](https://github.com/pop-os/cosmic-files/pull/1532) | **Smart open button** | Preview panel only shows "Open" when an app can open it |
| [#1520](https://github.com/pop-os/cosmic-files/pull/1520) | **Multi-select permissions** | Select multiple files → Right-click → "Properties" |
| [#1507](https://github.com/pop-os/cosmic-files/pull/1507) | **Location bar copy/paste** | Ctrl+C/Ctrl+V now works in the location bar |
| [#1490](https://github.com/pop-os/cosmic-files/pull/1490) | **Don't thumbnail thumbnails** | Automatic - prevents recursive thumbnail generation |
| [#1429](https://github.com/pop-os/cosmic-files/pull/1429) | **Bulk rename** | Select multiple files → Press F2 → Template rename dialog |
| [#1410](https://github.com/pop-os/cosmic-files/pull/1410) | **Prevent suspension** | Automatic - system won't sleep during file operations |
| [#1370](https://github.com/pop-os/cosmic-files/pull/1370) | **Shift+copy path** | Hold Shift while right-clicking → "Copy" becomes "Copy path" |
| [#1341](https://github.com/pop-os/cosmic-files/pull/1341) | **Thumbnail mode** | Settings → Control thumbnails (local/network/never) |
| [#857](https://github.com/pop-os/cosmic-files/pull/857) | **Multi-select preview** | Select multiple items → Preview shows file/folder count |

### Skipped PRs (Conflicts/API Issues)

| PR | Feature | Reason Skipped |
|----|---------|----------------|
| [#1535](https://github.com/pop-os/cosmic-files/pull/1535) | Tab drag-and-drop | libcosmic API changed - merged but drag feature disabled |
| [#780](https://github.com/pop-os/cosmic-files/pull/780) | Enhanced terminal & MIME | Jan 2025, too many conflicts, feature incomplete |
| [#659](https://github.com/pop-os/cosmic-files/pull/659) | Navigate by typing | Nov 2024, 9 conflicts across app.rs/tab.rs |
| [#574](https://github.com/pop-os/cosmic-files/pull/574) | Restore last session | Oct 2024, 5+ file conflicts, codebase diverged |

---

## Installation

### Build from this branch

```bash
# Clone this fork
git clone https://github.com/Lcstyle/cosmic-files.git
cd cosmic-files

# Checkout the feature bundle branch
git checkout feature-bundle

# Build
cargo build --release

# Install to /usr/local/bin (takes precedence over system version)
sudo cp target/release/cosmic-files /usr/local/bin/
```

### Verify installation

```bash
which cosmic-files
# Should show: /usr/local/bin/cosmic-files
```

### Revert to system version

```bash
sudo rm /usr/local/bin/cosmic-files
```

---

## Commit History

This branch is based on `upstream/master` (commit 8a63654) with the following merges:

```
b1f069a docs: add local build documentation
abdaa48 Fix duplicate imports and disable tab drag (API incompatible)
667d294 Merge PR #857 (Multiple selection preview page)
9a47dce Merge PR #1341 (Thumbnail mode option)
271491d Merge PR #1370 (Copy path when pressing Shift)
419df46 Merge PR #1410 (Prevent suspension during file ops)
0dfa23f Merge PR #1429 (Bulk rename dialog)
784df88 Merge PR #1490 (Don't thumbnail thumbnails)
a594145 Merge PR #1507 (Location bar copy/paste fix)
b88a908 Merge PR #1520 (Open-with & permissions for multi-select)
25047ac Merge PR #1532 (Smart open button)
59e977d Merge PR #1533 (Paste images/videos/text from clipboard)
01b3d5c Merge PR #1534 (File checksums)
be8f228 Merge PR #1535 (Tab drag-and-drop)
7db6ccf Merge PR #1564 (Copy file path)
0173974 feat(context-menu): add create desktop entry for executables
```

### Post-Merge Fixes

- Removed duplicate imports (`OperationError`, `OperationErrorType`, `Config`, `tab::Item`)
- Disabled `enable_tab_drag()`, `on_reorder()`, `tab_drag_threshold()` due to libcosmic API changes

---

## Branch Policy

- **DO NOT** submit PRs from this branch to upstream
- **DO NOT** merge upstream master directly (use rebase)
- This branch is for **local builds only**

### Updating this branch

```bash
git fetch upstream
git rebase upstream/master
# Resolve conflicts if any
cargo build --release
sudo cp target/release/cosmic-files /usr/local/bin/
```

---

## Contributing Back

If you want to help get stale PRs merged:

1. Create a new branch from `upstream/master`
2. Cherry-pick or rebase the PR commits
3. Fix conflicts
4. Submit a new PR referencing the original

---

## Credits

Features in this bundle were authored by:
- [@Lcstyle](https://github.com/Lcstyle) - Create desktop entry (#1568)
- [@orta](https://github.com/orta) - Copy file path (#1564)
- [@FreddyFunk](https://github.com/FreddyFunk) - Checksums (#1534), Clipboard paste (#1533), Shift+copy path (#1370)
- [@michaelmeuli](https://github.com/michaelmeuli) - Smart open button (#1532)
- [@jpttrssn](https://github.com/jpttrssn) - Multi-select permissions (#1520)
- [@JayDoubleu](https://github.com/JayDoubleu) - Location bar fix (#1507)
- [@joshuamegnauth54](https://github.com/joshuamegnauth54) - Don't thumbnail thumbnails (#1490), Prevent suspension (#1410)
- [@Kl4V3](https://github.com/Kl4V3) - Bulk rename (#1429)
- [@infifox](https://github.com/infifox) - Thumbnail mode (#1341)
- [@thatdevsherry](https://github.com/thatdevsherry) - Multi-select preview (#857)
- [@wash2](https://github.com/wash2) - Tab improvements (#1535, partial)

---

# cosmic-files
File manager for the COSMIC desktop environment

## Build the project from source

```sh
# Clone the project using `git`
git clone https://github.com/pop-os/cosmic-files
# Change to the directory that was created by `git`
cd cosmic-files
# Build an optimized version using `cargo`, this may take a while
cargo build --release
# Run the optimized version using `cargo`
cargo run --release
```

## Community and Contributing

The COSMIC desktop environment is maintained by System76 for use in Pop!_OS. A list of all COSMIC projects can be found in the
[cosmic-epoch](https://github.com/pop-os/cosmic-epoch) project's README. If you would like to discuss COSMIC and Pop!_OS, please
consider joining the [Pop!_OS Chat](https://chat.pop-os.org/). More information and links can be found on the
[Pop!_OS Website](https://pop.system76.com).

## License

This project is licensed under [GPLv3](LICENSE)
