# v1.1.0

IMPROVEMENTS
- Added concurrency settings for upload and download, which allow loading table data in parallel for each table and each disk for multi-disk storages
- Up go to 1.16
- Updated go libraries dependencies to actual version (exclude azure)
- Add Clickhouse 21.8 to test matrix
- remove `S3_PART_SIZE` config parameter and calculate it depends on `MAX_FILE_SIZE`
- improve logging for delete operation
- Added `S3_DEBUG` option to allow debug S3 connection
- Decrease number of SQL queries to system.* during backup commands
- Added options for RBAC and CONFIGs backup, look to `clickhouse-backup help create` and `clickhouse-backup help restore` for details
- Add `S3_CONCURRENCY` option to speedup backup upload
- Add `--diff-from-remote` to `upload` command for avoid store local backup

BUG FIXES
- fix [#256](https://github.com/AlexAkulov/clickhouse-backup/issues/256)
- backup only database metadata for proxy integrated database engines like MySQL, PostgreSQL fix [#223](https://github.com/AlexAkulov/clickhouse-backup/issues/223)
- Remove unused `SKIP_SYNC_REPLICA_TIMEOUTS` option

# v1.0.0

BUG FIXES
- Fixed silent cancel uploading when table has more than 4k files  (fix [#203](https://github.com/AlexAkulov/clickhouse-backup/issues/203), [#163](https://github.com/AlexAkulov/clickhouse-backup/issues/163). Thanks [mastertheknife](https://github.com/mastertheknife))
- Fixed download error for `zstd` and `brotli` compression formats
- Fixed bug when old-format backups hadn't cleared

# v1.0.0-beta2

IMPROVEMENTS

- Added diff backups
- Added retries to restore operation for resolve complex tables dependencies (Thanks [@Slach](https://github.com/Slach))
- Added SFTP remote storage (Thanks [@combin](https://github.com/combin))
- Now databases will be restored with the same engines (Thanks [@Slach](https://github.com/Slach))
- Added `create_remote` and `restore_remote` commands
- Changed of compression format list. Added `zstd`, `brotli` and disabled `bzip2`, `sz`, `xz`

BUG FIXES
- Fixed empty backup list when S3_PATH and AZBLOB_PATH is root
- Fixed azblob container issue (Thanks [@atykhyy](https://github.com/atykhyy))


# v1.0.0-beta1

IMPROVEMENTS

- Added 'allow_empty_backups' and 'api.create_integration_tables' options
- Wait for clickhouse in server mode (fix [#169](https://github.com/AlexAkulov/clickhouse-backup/issues/169))
- Added Disk Mapping feature (fix [#162](https://github.com/AlexAkulov/clickhouse-backup/issues/162))

BUG FIXES

- Fixed 'ftp' remote storage ([#164](https://github.com/AlexAkulov/clickhouse-backup/issues/164))

# v0.6.5

**It is the last release of v0.x.x**

IMPROVEMENTS
- Added 'create_remote' and 'restore_remote' commands
- Changed update config behavior in API mode

BUG FIXES
- fix [#154](https://github.com/AlexAkulov/clickhouse-backup/issues/154)
- fix [#165](https://github.com/AlexAkulov/clickhouse-backup/issues/165)

# v1.0.0-alpha1

IMPROVEMENTS
- Support for new versions of ClickHouse ([#155](https://github.com/AlexAkulov/clickhouse-backup/issues/155))
- Support of Atomic Database Engine ([#140](https://github.com/AlexAkulov/clickhouse-backup/issues/140), [#141](https://github.com/AlexAkulov/clickhouse-backup/issues/141), [#126](https://github.com/AlexAkulov/clickhouse-backup/issues/126))
- Support of multi disk ClickHouse configurations ([#51](https://github.com/AlexAkulov/clickhouse-backup/issues/51))
- Ability to upload and download specific tables from backup
- Added partitions backup on remote storage ([#83](https://github.com/AlexAkulov/clickhouse-backup/issues/83))
- Added support for backup/upload/download schema only ([#138](https://github.com/AlexAkulov/clickhouse-backup/issues/138))
- Added new backup format select it by `compression_format: none` option

BROKEN CHANGES
- Changed backup format
- Incremental backup on remote storage and 'flashback' feature is not supported now, but will supported in future versions

# v0.6.4

IMPROVEMENTS
- Added `CLICKHOUSE_AUTO_CLEAN_SHADOW` option for cleaning shadow folder before backup. Enabled by default.
- Added `CLICKHOUSE_SYNC_REPLICATED_TABLES` option for sync replicated tables before backup. Enabled by default.
- Improved statuses of operations in server mode

BUG FIXES
- Fixed bug with semaphores in server mode

