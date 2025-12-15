# Version Command

Display the current version of phpkg installed on your system.

---

## Overview

The `phpkg version` command shows you the version number of the phpkg installation, along with copyright information. This is useful for:
- Verifying your installation
- Checking which version you're running
- Troubleshooting version-related issues
- Reporting bugs (include version info)

---

## Usage

```bash
phpkg version
```

**Output**: Displays the phpkg logo, version number, and copyright information.

---

## Examples

### Basic Usage

```bash
$ phpkg version

██████╗ ██╗  ██╗██████╗ ██╗  ██╗ ██████╗ 
██╔══██╗██║  ██║██╔══██╗██║ ██╔╝██╔════╝ 
██████╔╝███████║██████╔╝█████╔╝ ██║  ███╗
██╔═══╝ ██╔══██║██╔═══╝ ██╔═██╗ ██║   ██║
██║     ██║  ██║██║     ██║  ██╗╚██████╔╝
╚═╝     ╚═╝  ╚═╝╚═╝     ╚═╝  ╚═╝ ╚═════╝ 

✅ phpkg version 3.0.0
Copyright (c) 2022-2025 PHPKG
```

---

## When to Use

### Verify Installation

After installing phpkg, verify it's working:

```bash
phpkg version
```

If you see the version output, phpkg is installed correctly.

### Check Version for Support

When reporting issues or asking for help, include your phpkg version:

```bash
phpkg version
# Output: phpkg version 3.0.0
```

### Troubleshooting

If commands aren't working, check your version:

```bash
phpkg version
```

This helps identify if you're running an outdated version that might need updating.

---

## Related Commands

- **[Installation](https://phpkg.com/documentations/installation)** - Learn how to install phpkg
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions

---

## Notes

- The version is read from phpkg's internal `config.json` file
- Version follows semantic versioning (major.minor.patch)
- Copyright year updates automatically based on the current year

