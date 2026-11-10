# only-what-was-asked

**"Pause only Google Ads" means only Google Ads. This skill makes the agent prove it.**

`only-what-was-asked` is an agent skill for Claude Code (and any agent that reads `SKILL.md` skills) for changes to live systems: ad accounts, campaigns, budgets, apps, chat bots, phone numbers, scheduled posts, websites, automations. The owner names one thing. The agent "tidies up" the rest: it pauses the Meta ads too "to be consistent", turns off the client's app because the invoice is late, or writes a rule that starts switching clients off a week later.

With the skill, the agent pins the target in one line (client, platform, account, object, action) and writes a do-not-touch list with each item's current state. It changes only the target, then reads back the target **and every neighbour** to prove nothing else moved. It also looks for automations that could do more later: auto-pause rules, cron jobs, "turn off after N days unpaid" logic. When it writes that kind of logic itself, the default is notify, never act.

## See the difference

> **Owner:** "Pause only Ana's Google Ads, she hasn't paid. Not Facebook, nothing else. And tell me how much it has spent."

**Without the skill:** it pauses the campaigns, checks that Meta and the app are still on, and reports the spend. It takes no before snapshot, and it does not look for rules or scripts that could switch more things off later.

**With the skill:**

> Target: Ana · Google Ads · her account · 2 active campaigns · pause.
> Do not touch: 3 Meta ad sets (active), WhatsApp app (on), other clients.
> Done 10:42 (UTC-6): 2 campaigns paused, MX$318 spent this month. Checked after: Meta 3 ad sets active, app on. Automations: none found that would act on her. Note: the late payment is your call; nothing else was changed for it.

On "Turn off Luis's search campaign" when Luis has two accounts, both runs ask which one. With the skill it is a rule, not luck.

**Skip it if** you are refactoring code in a repo: use a code blast-radius skill for that.

**Status:** new. Built from five real orders in the author's own setup ("only Google Ads, not Facebook", "the console must not turn anything off", "don't pause, turn on or change budgets without asking"). Tested with and without the skill on 3 cases: 6/6 with it, 5/6 without. The run without it took no before snapshot and did not switch the overdue rule to notify-only. Plain instructions, no scripts, no network calls. MIT. Issues and suggestions welcome.

## Install

With the [skills CLI](https://skills.sh):

```bash
npx skills add RabbitDesigns22/only-what-was-asked
```

Or manually: copy `skills/only-what-was-asked/` into `~/.claude/skills/` for all your projects, or into `.claude/skills/` for one project.

## Works well with

- [`published-vs-planned`](https://github.com/RabbitDesigns22/published-vs-planned): after cancelling or changing a scheduled post, check what is really live.
- [`small-budget-ads`](https://github.com/RabbitDesigns22/small-budget-ads): rules for which ad to turn off when the budget is small.

## Español

**Solo lo que pidió.** "Pausa solo el Google Ads" es solo Google Ads. El agente escribe en una línea qué va a cambiar (cliente, plataforma, cuenta, objeto, acción) y la lista de lo que no se toca con su estado de antes. Cambia solo eso y después revisa lo cambiado y todo lo de al lado para probar que nada más se movió. También busca reglas o scripts que puedan apagar algo solos más adelante. Si escribe una de esas reglas, por defecto solo avisa y nunca apaga.

Instalar: `npx skills add RabbitDesigns22/only-what-was-asked`

## More skills from the same setup

These come from one real workflow: a small agency run with 15+ Claude Code sessions in parallel. Each skill fixes one problem that kept happening there.

| Skill | What it fixes |
|---|---|
| [one-pass](https://github.com/RabbitDesigns22/one-pass) | get it right the first time; stop paying tokens for rework |
| [hora-exacta](https://github.com/RabbitDesigns22/hora-exacta) | real date and time in every message, so nothing lands on the wrong day |
| [hands-on](https://github.com/RabbitDesigns22/hands-on) | the agent does what it can and only asks you for codes, keys and payments |
| [easy-for-them](https://github.com/RabbitDesigns22/easy-for-them) | steps people actually follow: direct link, one action per line |
| [one-answer](https://github.com/RabbitDesigns22/one-answer) | one thought-through answer instead of plan, fix, new plan |
| [never-twice](https://github.com/RabbitDesigns22/never-twice) | a shared error log so no session repeats a known mistake |
| [sort-me-out](https://github.com/RabbitDesigns22/sort-me-out) | one ordered list of what is urgent, waiting and forgotten |
| [in-the-loop](https://github.com/RabbitDesigns22/in-the-loop) | a live board so parallel sessions know what the others changed |
| [study-first](https://github.com/RabbitDesigns22/study-first) | reads everything in full and answers point by point, no invented details |
| [session-watchdog](https://github.com/RabbitDesigns22/session-watchdog) | wakes the sessions that got stuck mid-task, leaves the rest alone |
| [skill-harvest](https://github.com/RabbitDesigns22/skill-harvest) | reads your sessions and finds the skills you are missing |
| [small-budget-ads](https://github.com/RabbitDesigns22/small-budget-ads) | Meta Ads rules for 1-5 USD a day ad sets |
| [whatsapp-closer](https://github.com/RabbitDesigns22/whatsapp-closer) | evidence-ranked rules for a WhatsApp sales assistant that closes |
| [whatsapp-number-onboarding](https://github.com/RabbitDesigns22/whatsapp-number-onboarding) | connect a number to the WhatsApp Cloud API in the safe order |
| [proposal-pdf](https://github.com/RabbitDesigns22/proposal-pdf) | short PDF proposals with every price checked against its source |
| [published-vs-planned](https://github.com/RabbitDesigns22/published-vs-planned) | says "published" only for what it saw live on the public page, Facebook and Instagram checked apart |
| [source-every-fact](https://github.com/RabbitDesigns22/source-every-fact) | every price, phone and name on a post traced to its source, nothing added |
| [only-what-was-asked](https://github.com/RabbitDesigns22/only-what-was-asked) | "pause only Google Ads" pauses only Google Ads, and proves the rest did not move |

If one of them saved you a redo, a star helps other people find it.

## License

MIT. Made by [Rabbit Designs](https://github.com/RabbitDesigns22).
