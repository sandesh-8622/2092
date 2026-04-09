# 2092

2092 is a personal assistant that runs entirely through Claude Code in the terminal. You open the folder, start Claude, and just talk to it. It remembers who you are across sessions, tracks whatever priorities you set, manages your schedule and finances, takes notes, and checks in on you like someone who actually knows your life. There is no web app, no dashboard, and no install. The whole thing is markdown and YAML files that Claude reads and writes to.

The name comes from Mr. Nobody, the year Nemo Nobody dies. The idea is that every choice you make leads to a different future and this tool helps you see where yours is going based on what you're actually doing day to day.

---

## Why I Built This

I wanted something that felt less like an app and more like a person keeping track of things for me. Every productivity tool I've tried either dies after a week because it feels like a chore, or it tracks numbers without understanding context. I didn't want a habit tracker that shows me a red square when I miss a day. I wanted something that knows my schedule, knows I have homework due on Wednesdays, knows I haven't eaten if it's 9pm and I haven't mentioned food, and can tell me where I'm heading if I keep doing what I'm doing.

The idea behind the architecture is simple. Claude Code already reads markdown files in whatever folder you open it in, so instead of building a separate app with its own UI and dependencies, the entire system is just well-structured instructions that Claude follows. No code, no runtime, no install. You talk to it in the terminal and it does everything through plain text files that you own and can read yourself.

---

## How It Works

The first time you open the folder in Claude Code, it doesn't know anything about you. It asks your name, what you do, what your priorities are, what your week looks like, and anything else you want to share. All of that goes into a file called MEMORY.md which gets loaded at the start of every session. That file is how it remembers you. It grows over time as you talk to it more.

There are also daily notes that get written after every conversation. These are short files in a memory folder, one per day, with what happened, how you seemed, what you mentioned, and anything unresolved. Today's and yesterday's notes get loaded every session so the assistant has immediate context. Over time the daily notes get consolidated into MEMORY.md so the important stuff survives long term.

The system is designed to deepen over time. Week one it knows your name and your priorities. Month one it knows your patterns and who the people in your life are. Month three it knows when you're lying to yourself about doing something tomorrow and it knows the difference between a bad day and a bad week. Month six it knows you well enough to connect things from months ago to what's happening now.

---

## What It Can Do

**Check-ins.** You set your own priorities during setup. Could be gym, job applications, homework, calling your mom, saving money, whatever matters to you. When you say "check in" it goes through each one and asks the question you chose. It tracks streaks and mentions when things are slipping or when you're on a roll. You don't have to do a formal check-in though, you can just start talking about your day and it will figure out what maps to which priority.

**Schedule.** It knows your weekly rhythm and specific upcoming events. If you tell it you have a midterm on Friday it will bring it up before Friday. If you tell it homework is always due on Wednesdays it will ask about it on Wednesday without you having to remind it.

**Finances.** Mention spending or earning and it logs it. Ask how you're doing on money and it gives you category breakdowns and comparisons to last month. It doesn't judge every purchase but it will tell you when a pattern is forming.

**Notes.** Say "save this as a note" or "add to my CS301 notes" and it creates or appends to a markdown file in the notes folder. You can ask to see notes on any topic and it pulls them up.

**Files.** Share any file at any time. Images, videos, PDFs, screenshots, code, whatever. It logs the file, looks at images, reads documents when relevant, and connects them to your priorities.

**Projections.** Once it has enough data it can show you where your current trajectory leads. If you've been applying to two jobs a week it can tell you how many applications you'll have out in three months and whether that's enough based on typical response rates. Not to scare you, just to give you the math so you can decide.

**Reports.** Ask for a weekly or monthly summary and it generates one. Completion rates, streak records, mood trends, patterns it noticed, and a few observations based on your actual data.

**Reminders.** Claude Code doesn't have a scheduler built in, so reminders work on a pull basis. Every session it checks if anything is due. If you want it to actually reach out to you at specific times you can set up a scheduled task on your system that opens Claude Code automatically.

---

## The Memory System

This is the part that makes it different from anything else. The memory has three layers.

First is MEMORY.md, the long-term memory. This is a structured file that contains everything the assistant knows about you. Not just facts but understanding. Who you are, what drives you, what you avoid, the people in your life, patterns it has noticed, your wins, your struggles, how you like to be supported in different situations. This file gets loaded every session and updated after every conversation.

Second is daily notes, one markdown file per day in the memory folder. These capture what happened in each session. What you checked in on, how you seemed, what you mentioned, open threads that weren't resolved. These are the raw observations.

Third is consolidation. Every week or so the assistant reads through the daily notes and promotes the important patterns and facts into MEMORY.md. Daily notes are the short-term memory. MEMORY.md is the refined understanding. Without consolidation you have data but no depth.

The key design decision is that temporary moods are never stored as permanent preferences. If you say "be brutal with me" on a confident day, that doesn't become a permanent rule. It gets stored as context for that day. Next week when you're stressed about an exam, the assistant reads the room and adjusts. It figures out how to talk to you based on your current state, your history, and what's happening in your life, not based on a setting you configured once.

---

## Setup

```bash
cd 2092
claude
```

First time it walks you through everything. After that you just talk.

For automated check-ins you can set up a scheduled task. On Windows:

```cmd
schtasks /create /tn "2092-morning" /tr "cd /d C:\path\to\2092 && claude -p \"morning check-in\"" /sc daily /st 09:00
```

On macOS or Linux:

```bash
# crontab -e
0 9 * * * cd ~/2092 && claude -p "morning check-in"
```

---

## Project Structure

```
2092/
    CLAUDE.md              The system prompt. Personality, rules, onboarding flow.
    MEMORY.md              Long-term memory. Grows over time.
    memory/                Daily notes, one file per day.
    config/
        profile.yml        Basic identity info.
        priorities.yml     What you're tracking and the check-in questions.
        reminders.yml      Scheduled nudges.
    data/
        checkins.tsv       Every check-in response logged.
        schedule.md        Weekly rhythm and upcoming events.
        finances.md        Spending and income log.
        notes/             Markdown files organized by topic.
        attachments.md     Log of every file shared.
    modes/                 Instructions for each type of interaction.
    reports/               Generated weekly and monthly summaries.
```

All data is plain text. Checkins are TSV, everything else is markdown or YAML. No databases, no dependencies. You can open any file in a text editor, grep through your history, or export everything whenever you want.

---

## License

MIT
