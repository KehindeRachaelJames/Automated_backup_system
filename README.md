# System Backup Script

A simple Bash script that automates Linux server backups. It creates compressed archives of important directories, generates checksums, and removes old backups automatically.

## Features

- Creates timestamped, compressed backups.
- Generates SHA-256 checksums for verification.
- Supports custom backup locations.
- Automatically removes old backups.
- Includes a dry-run mode.

## Requirements

Bash and standard Linux utilities. Root privileges are required to run a backup.

## Getting Started

Make the script executable:

```bash
chmod +x system-backup.sh
```

Preview the backup process:

```bash
sudo ./system-backup.sh --dry-run
```

Create a backup:

```bash
sudo ./system-backup.sh
```

## Options

| Option | Description |
|---|---|
| `--dry-run` | Preview actions without making changes. |
| `--destination DIR` | Set the backup location. |
| `--retention DAYS` | Set how long backups are kept. |
| `--help` | Show available options. |

Example:

```bash
sudo ./system-backup.sh \
  --destination /mnt/backups \
  --retention 14
```

By default, backups are saved to `/var/backups/system-backup` and retained for seven days.

## What Gets Backed Up?

The script backs up these directories when they exist:

- `/etc` — System configuration
- `/home` — User files
- `/root` — Root user files
- `/var/www` — Website files
- `/opt` and `/srv` — Application and service data

You can modify the `BACKUP_PATHS` array in the script to change what gets backed up.

## Notes

- This is a file-level backup, not a complete system image.
- Databases may require separate backup procedures.
- Store backups on a separate drive or remote server to protect against disk failure.
- Regular scheduling through cron or a systemd timer is not configured by the script.
