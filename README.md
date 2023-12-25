# BTRFS Snapshot Rotation Script

## Overview

This Bash script automates the process of managing BTRFS snapshots by creating, rotating, and deleting snapshots based on a specified retention policy. It is designed to be used as a scheduled task, such as a cron job, to ensure regular and controlled snapshot management.

## Features

- **Dependency Checks**: Verifies the presence of required dependencies (`btrfs` and `stat`) and exits with an error if they are not found.

- **Argument Validation**: Ensures that the script is provided with the necessary arguments: `filesystem`, `name`, and `count`. Displays usage information if arguments are missing or invalid.

- **Snapshot Rotation**: Maintains a specified number of snapshots by rotating older snapshots. Snapshots are named with a base name and an incrementing index.

- **Usage Examples**: Provides usage examples for different scheduling scenarios using cron jobs.

## Usage

### Script Invocation

```bash
./btrfs-snapshot-rotation.sh filesystem name count
```

- `filesystem`: The BTRFS filesystem or subvolume for which snapshots will be managed.
- `name`: The base name for the snapshots (e.g., hourly, nightly, weekly).
- `count`: The number of snapshots to be retained.

### Example Cron Jobs

```bash
# Run every hour and keep the last 24 hourly snapshots
@hourly ./btrfs-snapshot-rotation.sh /data/Temp hourly 24

# Run daily at midnight and keep the last 31 nightly snapshots
@midnight ./btrfs-snapshot-rotation.sh /data/Temp nightly 31

# Run monthly and keep the last 12 monthly snapshots
@monthly ./btrfs-snapshot-rotation.sh /data/Temp monthly 12

# Run weekly on Monday at midnight and keep the last 4 weekly snapshots
0 0 * * 1 ./btrfs-snapshot-rotation.sh /data/Temp weekly 4
```

## Requirements

- BTRFS filesystem with the `btrfs` command available.
- `stat` command for obtaining filesystem information.

## Important Notes

- This script assumes that the provided filesystem is a BTRFS filesystem, and the BTRFS-related commands are available.

- Make sure the script is executable (`chmod +x btrfs-snapshot-rotation.sh`) before using it.

- It is recommended to review and understand the script's logic before deploying it to production systems.

## Author

This script was written by [Your Name].

## License

This script is released under the [LICENSE] license. See the [LICENSE] file for more details.

[Your Name]: <your@email.com>
[LICENSE]: LICENSE.md
