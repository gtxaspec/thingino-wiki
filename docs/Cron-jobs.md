cron is a job scheduler that runs predefined commands at a preset time.

To edit the list of cron jobs, run `crontab -e` in console.

```
#  .---------------- minute
#  |  .------------- hour
#  |  |  .---------- day
#  |  |  |  .------- month 
#  |  |  |  |  .---- day of week (0-7 or sun,mon,tue,wed,thu,fri,sat)
#  |  |  |  |  |     command
#
#  *  *  *  *  *     /path/to/script -foo -bar
```

Each job is defined as a line of parameters where

- **minute** is a number from `0`to `59`, or a period (e.g. `*/10` for _every 10 minutes_).
- **hour** is a humber from `0` to `23`.
- **day** is the day of the month, a number from `1` to `31`.
- **month** is a number from `1` to `12`, or a three-letter abbreviation: `jan`, `feb`, `mar`, `apr`, `may`, `jun`, `jul`, `aug`, `sep`, `nov`, `dec`.
- **day of week** is a number from `0` (for Sunday) to `7` (for Sunday again).
- **command** is a path to the script to be executed, with optional arguments.

