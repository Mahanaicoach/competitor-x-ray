# Installing Competitor X-Ray

Two ways to install, depending on how you use Claude. Pick the one that matches you.

---

## Option A — Claude desktop app (Cowork) ✅ easiest

This is the method most people want.

1. On this repo's main page, click the file **`competitor-x-ray.skill`**.
2. On the file page, click the **Download** button (or the download icon) to save it to your computer.
3. Open the **Claude desktop app**.
4. Drag the `competitor-x-ray.skill` file into a chat (or open it), then click **Save skill**.
5. Done. Start a chat and paste your competitors — Claude loads the skill automatically.

> The `.skill` file is just a zipped bundle of everything in the `competitor-x-ray/` folder. You don't need to unzip anything yourself.

---

## Option B — Claude Code (CLI / terminal)

If you run Claude Code from your terminal, copy the skill folder into your skills directory.

```bash
# 1. Clone this repo
git clone https://github.com/mahanaicoach/competitor-x-ray.git

# 2. Copy the skill folder into your Claude Code skills directory
cp -r competitor-x-ray/competitor-x-ray ~/.claude/skills/
```

That's it. Claude Code discovers skills in `~/.claude/skills/` on the next run.

> Your skills directory may differ. Common locations:
> - User-level: `~/.claude/skills/`
> - Project-level: `.claude/skills/` inside a specific project
>
> Copy the inner `competitor-x-ray/` folder (the one containing `SKILL.md`) — not the repo root.

---

## Optional: enable the designed-PDF report

The fanciest output format (a branded, visual intelligence brief) renders with **WeasyPrint**. Everything else — chat summary, spreadsheet, Word doc — works without it.

```bash
pip install weasyprint
```

On some systems you may need:

```bash
pip install weasyprint --break-system-packages
```

If WeasyPrint won't install, the skill automatically falls back to ReportLab (already present in most environments) and produces the same report structure.

---

## Optional: the `/x-ray` slash command (Claude Code)

The skill triggers automatically from plain language — you don't need a command. But if you want a one-liner shortcut in **Claude Code**, this repo ships one:

```bash
# from inside the cloned repo
cp commands/x-ray.md ~/.claude/commands/x-ray.md
```

Then you can run it directly:

```
/x-ray @sabrina_ramonov @thedankoe gregisenberg
```

It tells Claude to invoke the competitor-x-ray skill on whatever targets you pass (or asks for them if you leave it blank). This is a Claude Code feature — the Cowork desktop app uses plain-language triggering instead.

---

## Verify it's working

Open a chat and paste:

```
research these competitors for me: @sabrina_ramonov @thedankoe
```

If the skill is installed, Claude will ask you which **output format** you want (PDF / chat / spreadsheet / Word) and then start researching each competitor in parallel. If it doesn't, double-check the install step above.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Claude doesn't trigger the skill | Make sure you saved/copied it correctly (Step above). Try being explicit: *"use the competitor-x-ray skill on …"* |
| PDF output fails | Install WeasyPrint, or ask for the **chat** or **spreadsheet** format instead |
| A handle "can't be found" | The skill searches for corrected spellings. If it's genuinely private/gated, it pulls facts from the person's website, Linktree, podcasts, and analytics instead of guessing |
| Numbers look like estimates | That's intentional — gated profiles get **REPORTED** (estimated) tags, never fake-confirmed numbers |

---

Questions or want more builds like this? → [@mahanaicoach](https://instagram.com/mahanaicoach)
