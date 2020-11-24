# Day 10 : Timers and scheduling

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/10.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/comments/jt1yg9/day_10_getting_the_computer_to_do_your_work_for/) posts.

*video*

## Objectives of the day
1. **Cron and crontab**

```crontab -l```

```vim /etc/crontab```

```m``` - minute (0-59)

```h``` - hour (0-23)

```dom``` - day of the month (1-31)

```mon``` - month of the year (1-12)

```dow``` - day of the week (sun-sat)

```
@reboot   - after reboots
@yearly   "0 0 1 1 *"
@monthly  "0 0 1 * *"
@weekly   "0 0 * * 0"
@daily    "0 0 * * *"
@hourly   "0 * * * *"
```

2. **Timers** ```systemctl list-timers```
3. **Log Rotate**
4. **Journaling** ```journalctl```

For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
