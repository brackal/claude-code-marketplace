# claude-code-marketplace

Eigene Skills für Claude Code als Plugin-Marketplace `marketplace-brackal`, nach Zweck in Plugins gegliedert.
Ein Skill wird geladen, sobald seine Beschreibung zur Aufgabe passt, oder mit `/<plugin>:<skill>` aufgerufen.

| Plugin | Skills | Wofür |
| --- | --- | --- |
| [git](plugins/git/) | `conventional-commit` | Commit-Nachrichten nach Conventional Commits |

## Installation

In einer Kommandozeile, nicht im Chat von Claude Code:

```text
claude plugin marketplace add https://github.com/brackal/claude-code-marketplace.git
claude plugin install git@marketplace-brackal
```

## Weiterführendes

- [Lizenz](LICENSE)
