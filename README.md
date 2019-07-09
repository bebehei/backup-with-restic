# backup-with-restic

Backup tool to create easily repositories with [restic](https://restic.net/).

## Usage

```
backup do-backup
```

Create a new snapshot with your current configuration.

```
backup do-forget
```

Forget your snapshots according to `KEEP_*` variables in the configuration file.

```
backup (run)
backup
```

Create a new snapshot and then delete the repository snapshots. (Wraps `do-backup` and `do-forget`)

### Wrapper

You also can use native `restic` commands like `snapshots` or `mount`. These will respect the exported `RESTIC_*` variables. So a plain `backup snapshots` will list all of your current snapshots in the configured repository.

## Installation

You need to have [restic](https://restic.net) prior to your first run. See [restic's installations instructions](https://restic.readthedocs.io/en/stable/020_installation.html) for details.

    # install scripts
    git clone https://github.com/bebehei/backup-with-restic
    cd backup-with-restic
    make install
    cp /etc/backup/{example,default}.env

    # edit default.env to match backup data
    $EDITOR /etc/backup/default.env

    # initialize everything
    backup init

    # add cronjob (for hourly backup)
    { crontab -l ; echo "0 * * * * backup"; } | crontab -

**Hint: Depending on your configuration, you may need sudo for some commands.**
