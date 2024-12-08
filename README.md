# fstab-to-UUID

A robust Bash script that safely converts `/dev/sd*` device paths in `/etc/fstab` to their corresponding UUID format while preserving all other entries. This tool is particularly useful for system administrators and Linux users who want to ensure their system uses stable device identifiers.

## Features

- Selectively converts only standard SCSI/SATA disk devices (`/dev/sd*`)
- Preserves all other device entries (including `/dev/mapper/`, `/dev/disk/`, etc.)
- Dry-run mode to preview changes before applying
- Automatic backup creation before making changes
- Comprehensive error handling and privilege checking

## Installation

```bash
git clone https://github.com/ecrotty/fstab-to-UUID.git
cd fstab-to-UUID
chmod +x fstab-to-UUID.sh
```

## Usage

```bash
# Show help and usage information
./fstab-to-UUID.sh --help

# Preview changes without modifying fstab (dry-run mode)
./fstab-to-UUID.sh --dry-run

# Apply changes to fstab (requires root privileges)
sudo ./fstab-to-UUID.sh --write
```

### Command Line Options

- `-h, --help`: Show help message and usage information
- `-w, --write`: Write changes to `/etc/fstab` (requires root privileges)
- `-d, --dry-run`: Show what changes would be made without writing

## Safety Features

1. Automatic backup creation before any modifications
2. Dry-run mode for safe preview of changes
3. Root privilege verification for write operations
4. Preservation of comments and non-SCSI/SATA entries
5. UUID verification before replacement

## Example

Before:
```
/dev/sda1    /    ext4    defaults    0    1
/dev/sdb1    /home    ext4    defaults    0    2
```

After:
```
UUID=6197e068-5c43-4c3d-9a59-9a5c3c8ca867    /    ext4    defaults    0    1
UUID=4f2c4644-aaaa-bbbb-cccc-123456789abc    /home    ext4    defaults    0    2
```

## Requirements

- Linux operating system
- Bash shell
- Root privileges (for write mode only)
- `blkid` utility (typically pre-installed on Linux systems)

## Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting pull requests.

## License

This project is licensed under the BSD 3-Clause License - see the [LICENSE](LICENSE) file for details.

## Author

Ed Crotty (ecrotty@edcrotty.com)

## Support

For bug reports and feature requests, please use the GitHub issue tracker:
https://github.com/ecrotty/fstab-to-UUID/issues
