# learning-with-copilot

Agent skills for one-to-one tutoring, based on the **Alvar method** from Eero Alvar's
[How I Use AI to Learn Things](https://youtu.be/kzcI5F4tGiU).

| Skill | What it does |
|---|---|
| [`teach`](skills/teach) | Tutor: probe the edge of your understanding, plan a mermaid DAG, teach one reasoning step at a time, grade with delayed cold re-tests |
| [`probe`](skills/probe) | Short graded quiz that maps what you already know |
| [`learn-profile`](skills/learn-profile) | Interviews you and writes `alvar/LEARNER.md` |
| [`learn-verify`](skills/learn-verify) | Fact-checks a teaching claim against sources |
| [`learn-visual`](skills/learn-visual) | Makes a teaching diagram (usually SVG) and iterates until it shows the idea |
| [`learn-anki`](skills/learn-anki) | Turns a finished lesson into an Anki deck (needs an Anki MCP server) |

## Install

Copy the folders under `skills/` into your skills directory, e.g. `~/.claude/skills/`.

## Credits

- Method: Eero Alvar
- `teach`, `probe`, `learn-profile`, `learn-verify`, `learn-visual`: vasanthsreeram (MIT)
- `learn-anki`: mohamed (MIT)

See [LICENSE](LICENSE).
