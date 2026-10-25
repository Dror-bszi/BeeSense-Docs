# AGENTS.md – הנחיות לסוכני AI בעבודה על ה-vault

This folder is the **BeeSense** Obsidian vault (4th-year EE project, BGU), versioned in git.
Remote: `origin` → https://github.com/Dror-bszi/BeeSense-Docs.git · branch: `main`

## Rule: commit and push after every change
**After any write, edit, move, rename or delete of a file in this vault, commit and push immediately.**
Do not batch changes until the end of a session, and do not leave the vault with uncommitted work.

```bash
git pull --rebase origin main      # first, to pick up changes from other devices / Obsidian Git
git add -A
git commit -m "<short description of what changed>"
git push origin main
```

- **Commit message:** one short line in English or Hebrew describing the change
  (e.g. `hardware: add ESP32-S3 hub`, `PDR: update power budget`).
- **Conflicts:** if `pull --rebase` reports a conflict, stop and ask the user – never force-push
  (`--force`) and never discard someone else's changes.
- **Push fails** (no network, auth): tell the user that the change is committed locally but not pushed.
- **Respect `.gitignore`** – do not commit Obsidian workspace files or `.trash/`.

## כלל: push אחרי כל שינוי
אחרי כל כתיבה, עריכה, העברה, שינוי שם או מחיקה של קובץ ב-vault – לבצע מיד `pull --rebase`, `add`, `commit` ו-`push` ל-`main`.
לא לצבור שינויים לסוף העבודה. בהתנגשות (conflict) – לעצור ולשאול, לעולם לא `--force`.

## מבנה ה-vault
- `docs/` – תקציר (`abstract.md`) ודו"ח ה-PDR (`pdr-2027-165.docx`)
- `hardware/` – קטלוג הציוד: `README.md`, `inventory.csv`, `orders.md`, `components/`
- `software/` – הסבר על התוכנה (`README.md`); הקוד עצמו ב-repo נפרד: https://github.com/Dror-bszi/BeeSense (עותק מקומי: `\\wsl.localhost\Ubuntu\home\drorb\BeeSense`)
- `Instructions/` – נוהל הפרויקטים של המחלקה
- `refrence/` – PDR לדוגמה (PlayAble); `refrence/papers/` – קובצי המקורות של ה-PDR עם אינדקס (`README.md`)
- `TODO.md` – משימות פתוחות
