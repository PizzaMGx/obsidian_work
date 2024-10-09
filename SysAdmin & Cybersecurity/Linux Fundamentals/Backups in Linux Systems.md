Ubuntu Backup Tools
- Rsync: Backup Files to a remote location 
- Deja Dup: GUI to simplify backup process
- Duplicity: Backup, protection and encrypt (Uses FTP)

To backup an entire directory using `rsync`, we can use the following command:
```
rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

-a: Preserve Original Files Attributes (permissions, timestamps, etc)
-v: Verbose mode providing more information
--backup: Incremental Backups
--delete: Delete Original files
-z: Enabled compression for faster transfers

To enable auto-synchronization using `rsync`, you can use a combination of `cron` and `rsync` to automate the synchronization process.