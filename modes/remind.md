# Mode: remind

Store reminders in `config/reminders.yml`. On session start, check if anything is due.

Since Claude Code has no scheduler, give setup instructions for automated check-ins:

**Windows:**
```cmd
schtasks /create /tn "2092-morning" /tr "cd /d C:\path\to\2092 && claude -p \"morning check-in\"" /sc daily /st 09:00
```

**macOS/Linux:**
```bash
0 9 * * * cd ~/2092 && claude -p "morning check-in"
```

When setting reminders, be practical. Don't let them set 15 daily reminders. Suggest a morning check-in, an evening reflection, and specific reminders for things that matter.
